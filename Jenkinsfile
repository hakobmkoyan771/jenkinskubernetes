pipeline {
    agent none
    stages {
        stage('Run maven') {
            agent {
                kubernetes {
                    yaml '''
                    apiVersion: v1
                    kind: Pod
                    spec:
                        containers:
                            - name: maven
                              image: maven:3.8.1-jdk-8
                              command:
                              - sleep
                              args:
                              - 99d
                    '''
                }
            }
            steps {
                sh 'mvn -B -ntp clean install'
            }
        }
    }
}
