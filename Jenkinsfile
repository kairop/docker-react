pipeline {
    agent any
    parameters {
        choice(name: 'VERSION', choices: ['1.1.0','1.2.0','1.3.0'], description: '')
        booleanParam(name: 'executeTest', defaultValue: true, description: '')
    }
    tools {
        maven 'Maven'
    }
    stages {
        stage("build"){
            steps {
                echo 'building the application...'
                echo "mvn install"
            }
        }
        stage("test"){
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
                echo "deploying version ${VERSION}"
            }
        }
    }
}
