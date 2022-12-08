pipeline {
   
    agent any
   
    tools {nodejs "Node16"}
    
    parameters {
        choice(name: 'Scripts', choices: ['spec.cy.js', 'window.cy.js'])
        choice(name: 'BROWSER', choices: ['chrome', 'edge', 'firefox'])
    }
   

    //The stage directive goes in the stages section and should contain a steps section, an optional agent section, 
    //or other stage-specific directives. Practically speaking, all of the real work done by a Pipeline will be wrapped
    //in one or more stage directives.
    stages {
        
        stage('Build'){
            //The steps section defines a series of one or more steps to be executed in a given stage directive.
            steps {
                echo "Building the application"
            }
        }
        
        stage('Testing') {
            steps {
                sh """
                npm i
                npx cypress run --browser "${BROWSER}" --scripts "${scripts}"
                """
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
                publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: true, reportDir: 'cypress/report', reportFiles: 'index.html', reportName: 'HTML Report', reportTitles: ''])
        }
    }
}
