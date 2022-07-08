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
                          - sleep
                          args:
                          - 999999
            '''
        }
    }
    stages {
        stage('uxaki') {
            container('ubuntu') {
                steps {
                    sh 'sleep 999999'
                }
            }
        }
    }
}
