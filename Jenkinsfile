def gv

pipeline {
    /* agent any
         environment {
         NEW_VERSION = '1.2.0'
         SERVER_CREDENTIALS = credentials('server-credentials')
     } */
    parameters {
        // string(name: 'VERSION', defaultValue: '', description: 'version to deploy on prod ')
        choice(name: 'VERSION', choices: ['1.1.0', '1.2.0', '1.3.0'], description: '')
        booleanParam(name: 'executeTests', defaultValue: true, description: '')
    }
    stages {
        stage("init") {
            steps {
                script {
                   gv = load "script.groovy" 
                }
            }
        }
        stage("build") {
                        /* when {
                 expression {
                     BRANCH_NAME == 'dev' && CODE_CHANGES == true
                 }
             } */
            steps {
                script {
                    gv.buildApp()
                }
            }
        }
        stage("test") {
                        /* when {
                 expression {
                     BRANCH_NAME == 'dev' || BRANCH_NAME == 'master'
                 }
             } */
            when {
                expression {
                    params.executeTests
                }
            }
            steps {
                script {
                    gv.testApp()
                }
            }
        }
        stage("deploy") {
            steps {
                script {
                /* withCredentials([
                     usernamePassword(credentials: 'server-credentials', usernameVariable: USER, passwordVariable: PWD)
                 ]) {
                     sh "script ${USER} ${PWD}"
                 } */
                    gv.deployApp()
                }
            }
        }
    }   
    /* post {
         always {
             echo "hello"
         }
         success {
             echo "hello"
         }
         failure {
             echo "hello"
         }
    */ }
}
