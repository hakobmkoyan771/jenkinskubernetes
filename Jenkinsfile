pipeline {
    agent none
    stages {
        stage('Build default repo docker image') {
            agent {
                kubernetes {
                    yaml '''
                    apiVersion: v1
                    kind: Pod
                    metadata:
                        name: dind
                    spec:
                        containers:
                            - name: dind
                              image: docker:rc-git
                    '''
                }
            }
            steps {
                sh "git clone https://github.com/hakobmkoyan771/jenkinskubernetes.git"
                sh "docker build -t ap"
            }
        }
    }
}