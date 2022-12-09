pipeline {
   
    agent any
   
    tools {nodejs "Node16"}
    
    parameters {
        //string(name: 'SPEC', defaultValue: "cypress/e2e/")
        choice(name: 'BROWSER', choices: ['chrome', 'edge', 'electron'])
        choice(name: 'Scripts', choices: ['spec.cy.js', 'window.cy.js'])
    }
   
    stages {
        
        stage('Build'){
            //The steps section defines a series of one or more steps to be executed in a given stage directive.
            steps {
                echo "Building the application"
            }
        }
        
        stage('Testing') {
            steps {
                sh "npm i"
                sh "npm install cypress --save-dev"
                sh "npm install mocha"
                sh "npm install mochawesome"
                sh "npm install -D cypress-iframe"
                script {
                if (params.Scripts == "spec.cy.js")
                sh "npx cypress run --browser ${BROWSER} --spec cypress/e2e/spec.cy.js"
                else
                sh "npx cypress run --browser ${BROWSER} --spec cypress/e2e/window.cy.js"
                }
            }
        }
        
        stage('Deploy'){
            steps {
                echo "Deploying"
            }
        }
    }
        post {
        always {
                publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: true, reportDir: 'cypress', reportFiles: 'index.html', reportName: 'HTML Report', reportTitles: '', useWrapperFileDirectly: true])
        }
    }
}
