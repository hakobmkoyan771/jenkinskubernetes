pipeline {
    agent none
    stages {
        stage('a') {
            agent {
                kubernetes {
                    yaml: '''
                    apiVersion: v1
                    kind: Pod
                    metadata:
                        name: ubuntu
                    spec:
                        containers:
                            - name: ubuntu
                              image: ubuntu:alpine
                    '''
                }
                steps {
                    container('ubuntu') {
                        sh "hostname"
                    }
                }
            }
        }
        stage('b') {
            agent {
                kubernetes {
                    yaml:'''
                    apiVersion: v1
                    kind: Pod
                    metadata:
                        name: nginx
                    spec:
                        containers:
                            - name: nginx
                              image: nginx
                    '''
                }
                steps {
                    container('nginx') {
                        sh "hostname"
                    }
                }
            }
        }
    }
}
