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
                      image: gcr.io/kaniko-project/executor:debug
                      volumeMounts:
                        - name: docker-cred
                          mountPath: /kaniko/.docker
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
        stage('Build docker image and push to repository') {
            steps {
                container('kaniko') {
                    sh """/kaniko/executor --context `pwd` --destination hakobmkoyan771/app+${env.BUILD_NUMBER}"""
                }
            }
        }
    }
}
