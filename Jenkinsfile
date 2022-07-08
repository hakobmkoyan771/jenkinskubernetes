pipeline {
    agent none
    stages {
        stage('Build docker image and push to repo.') {
            agent {
                kubernetes {
                    yaml '''
                        apiVersion: v1
                        kind: Pod
                        metadata:
                            name: kaniko
                        spec:
                            containers:
                                - name: kaniko
                                  image: gcr.io/kaniko-project/executor:latest
                                  args: ["--context=git://github.com/hakobmkoyan771/jenkinskubernetes",
                                         "--destination=hakobmkoyan771/app:0.0.0"]
                                  volumeMounts:
                                    - name: kaniko-secret
                                      mountPath: /kaniko/.docker
                            restartPolicy: Never
                            volumes:
                              - name: kaniko-secret
                                secret:
                                  secretName: dockercred
                                  items:
                                    - key: .dockeconfigjson
                                      path: config.json
                    '''
                }
            }
            steps {
                sh '''
                /kaniko/executor --context `pwd` --destination hakobmkoyan771/app:0.0.0
                '''
            }
        }
    }
}
