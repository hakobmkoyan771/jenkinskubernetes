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
                    - name: ubuntu
                      image: ubuntu
                      command:
                        - "sleep"
                      args:
                        - "999999"
                """
        }
    }
    stages {
        stage('Build docker image') {
            steps {
                container(name: 'ubuntu') {
                    sh """
                        sleep 999999
                    """
                }
            }
        }
    }
}
