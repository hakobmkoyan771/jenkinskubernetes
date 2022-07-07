podTemplate(yaml:'''
    apiVersion: v1
    kind: Pod
    metadata:
        name: app
        labels:
            app: contact
    spec:
        containers:
            - name: app-contact
              image: hakobmkoyan771/contactpython:0.1.0
              ports:
                - containerPort: 80
''') {
    node(POD_LABEL) {
        stage('create file')
            container('app') {
                stage('create file') {
                    sh "touch ~/file"
                }
            }
        }
    }
}
