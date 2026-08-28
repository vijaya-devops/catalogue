pipeline {
    agent {
        node {
            label 'ROBOSHOP'
        }
    }

     environment {
        def appVersion =  ""
        acc_id = "389425628631"
        project = "roboshop"
        component = "catalogue"
     }

    options {
        disableConcurrentBuilds()
        timeout(time: 1, unit: 'MINUTES')
    }

    // parameters {
    //     string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
    //     text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')
    //     booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')
    //     choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')
    //     password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')
    // }

    stages {

        stage('Read version') {
            steps {
                script {
                    // Read and parse the JSON file from the workspace root
                    def packageJson = readJSON file: 'package.json'

                    // Access specific properties
                    appVersion = packageJson.version

                    echo "Application Version: ${appVersion}"
                }
            }
        }

        stage('Install dependencies') {
            steps {
                script {
                    sh """
                    npm install
                    """
                }
                
            }
        }

        stage('Docker Build') {
            steps {
                script {
                    // in this block we get aws authentication
                    withAWS(credentials: 'aws-creds', region: 'us-east-1') {
                    sh """   
                    aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin ${acc_id}.dkr.ecr.us-east-1.amazonaws.com
                    docker build -t ${acc_id}.dkr.ecr.us-east-1.amazonaws.com/${project}/${component}:${appVersion} .
                    docker push ${acc_id}.dkr.ecr.us-east-1.amazonaws.com/${project}/${component}:${appVersion}
                    """
                    }
                }
            }
        }

        stage('Deploy') {
            input {
                message "Should we continue?"
                ok "Yes, we should."
                submitter "alice,bob"

                parameters {
                    string(
                        name: 'PERSON',
                        defaultValue: 'Mr Jenkins',
                        description: 'Who should I say hello to?'
                    )
                }
            }

            steps {
                script {
                    echo 'Deploying....'
                }
            }
        }
    }

    post {
        always {
            echo 'I will always say Hello again!'
        }

        success {
            echo 'I will say Hello only if successful'
        }

        failure {
            echo 'I will say Hello only if failed'
        }
    }
}