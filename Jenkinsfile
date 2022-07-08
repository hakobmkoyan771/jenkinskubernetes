pipeline {
    agent   {
        kubernetes {
            yaml """
            apiVersion: v1
            kind: Pod
            metadata:
                name: app
            spec:
                containers:
                    - name: kaniko
                      image: ubuntu
                      command:
                        - "sleep"
                      args:
                        - "999999"
                      volumeMounts:
                        - name: docker-cred
                          mountPath: /kaniko/.docker
                """
        }
    }
    stages {
        stage('Build docker image') {
            steps {
                container(name: 'kaniko', shell: '/bin/bash') {
                    sh """
                        sleep 999999
                    """
                }
            }
        }
    }
}
