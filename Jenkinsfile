pipeline {
    agent {
        node {
            label 'ROBOSHOP'
        }
    }
        // environment {
        //    COURSE = 'Jenkins'
        // }
    options {
       
        disableConcurrentBuilds()
        timeout(time: 1, unit: 'MINUTES')
    }
    //  parameters {
    //     string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
    //     text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')
    //     booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')
    //     choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')
    //     password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')
    // }
    // build
    stages {
        stage('Build') {
            stage('Read version') {
                steps {
                    script {
                        script {
                    // Read and parse the JSON file from the workspace root
                    def packageJson = readJSON file: 'package.json'
                    
                    // Access specific properties
                    def appVersion = packageJson.version
                    echo "Application Version: ${appVersion}"
                    }
                }
            }
            steps {
                script {
                    
                    
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    echo 'Testing..'
                }
            }
        }
        stage('Deploy') {

             input {
                message "Should we continue?"
                ok "Yes, we should."
                submitter "alice,bob"
                parameters {
                    string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
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