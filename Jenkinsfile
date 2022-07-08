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
                      image: gcr.io/kaniko-project/executor
                      command:
                        - sleep
                      args:
                        - 9999999
                      volumeMounts:
                        - name: docker-cred
                          mountPath: /kaniko/.docker
                        - name: gitrepo
                          mountPath: /tmp
                initContainers:
                    - name: alpine
                      image: alpine
                      command: ["mkdir", "/tmp/git${env.BUILD_NUMBER}"]
                      volumeMounts:
                        - mountPath: /tmp
                          name: gitrepo
                    - name: git
                      image: bitnami/git
                      command: 
                        - "git"
                      args: ["clone", "https://github.com/hakobmkoyan771/jenkinskubernetes.git", "/tmp/git${env.BUILD_NUMBER}"]
                      volumeMounts:
                        - mountPath: /tmp
                          name: gitrepo
                volumes:
                    - name: gitrepo
                      hostPath:
                        path: /tmp
                    - name: docker-cred
                      secret:
                        secretName: dockercred
                        items:
                          - key: .dockerconfigjson
                            path: config.json
                """
        }
    }
    stages {
        stage('Build docker image') {
            steps {
                container(name: 'kaniko', shell: '/busybox/sh') {
                    sh """#!/busybox/sh
                        /kaniko/executor --dockerfile=/tmp/git${env.BUILD_NUMBER}/Dockerfile --context=/tmp/git${env.BUILD_NUMBER} --destination=hakobmkoyan771/app:0.1.0
                    """
                }
            }
        }
    }
}
