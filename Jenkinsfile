pipeline {
    agent {
        kubernetes {
            yaml '''
                apiVersion: v1
                kind: Pod
                spec:
                    containers:
                        - name: ubuntu
                          image: ubuntu
                          command:
                          - ls
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
