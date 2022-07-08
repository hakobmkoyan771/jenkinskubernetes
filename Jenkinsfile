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
                                  args: ["--dockerfile=./",
                                         "--context=git://github.com/hakobmkoyan771/jenkinskubernetes.git",
                                         "--no-push]
                                  volumeMounts:
                                    - name: kaniko-secret
                                      mountPath: /secret
                                  env:
                                    - name: GOOGLE_APPILICATION_CREDENTIALS
                                      value: /secret/kaniko-secret.json
                            restartPolicy: Never
                            volumes:
                              - name: kaniko-secret
                                secret:
                                  secretName: kaniko-secret
                    '''
                }
            }
            steps {
                sh "sleep 1"
            }
        }
    }
}
