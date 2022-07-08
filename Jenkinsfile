pipeline {
    agent {
        kubernetes {
            yaml '''
            apiVersion: v1
            kind: Pod
            metadata:
                name: app
            spec:
                containers:
                    - name: kaniko
                      image: gcr.io/kaniko-project/executor
                      command:
                      - ls
                      volumeMounts:
                        - name: docker-cred
                          mountPath: /kaniko/.docker
                        - name: gitrepo
                          mountPath: /tmp
                volumes:
                    - name: docker-cred
                      secret:
                        secretName: dockercred
                        items:
                          - key: .dockerconfigjson
                            path: config.json
            '''
        }
    }
    stages {
        stage('uxaki') {
            steps {
                container('ubuntu') {
                    sh 'ls'
                }
            }
        }
    }
}
