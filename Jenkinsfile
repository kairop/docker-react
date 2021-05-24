// CODE_CHANGES = getGitchanges()
// list of Env var were in http://localhost:8080/env-vars.html/
pipeline {
    agent any
    // environment {
    //     NEW_VERSION = '1.2.0'
    //     SERVER_CREDENTIALS = credentials('server-credentials')
    // }
    parameters {
        // string(name: 'VERSION', defaultValue: '', description: 'version to deploy on prod ')
        choice(name: 'VERSION', choices: ['1.1.0', '1.2.0', '1.3.0'], description: '')
        booleanParam(name: 'executeTests', defaultValue: true, description: '')
    }
    tools {
        maven 'Maven'
    }
    stages {
        stage("build"){
            // when {
            //     expression {
            //         BRANCH_NAME == 'dev' && CODE_CHANGES == true
            //     }
            // }
            steps {
                echo 'building the application...'
                // echo "building version ${NEW_VERSION}"
                echo "mvn install"
            }
        }
        stage("test"){
            // when {
            //     expression {
            //         BRANCH_NAME == 'dev' || BRANCH_NAME == 'master'
            //     }
            // }
            when {
                expression {
                    params.executeTests
                }
            }
            steps {
                echo 'testing the application...'
            }
        }
        stage("deploy"){
            steps {
                echo 'deploy the application...'
                // withCredentials([
                //     usernamePassword(credentials: 'server-credentials', usernameVariable: USER, passwordVariable: PWD)
                // ]) {
                //     sh "script ${USER} ${PWD}"
                // }
                echo "deploying version ${params.VERSION}"
            }
        }
    }
    // post {
    //     always {
    //         //
    //     }
    //     success {
    //         //
    //     }
    //     failure {
    //         //
    //     }
    // }
}
