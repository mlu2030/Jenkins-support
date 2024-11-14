
// CODE_CHANGES = true

pipeline {

    agent any

    parameters {
        choice(name: 'VERSION', choices: ['1.1.0', '1.2.0', '1.3.0'], description: '')
        booleanParam(name: 'executeTest', defaultValue: true, description: '')
    }

    // tool {
    //     maven 'Maven'
    // }

    environment {
        NEW_VERSION = '1.3.0'
        SERVER_CREDENTIALS = credentials('MDE101')
    }

    stages {

        stage("build") {
            when {
                expression {
                    BRANCH_NAME == 'develop' || env.BRANCH_NAME == 'main'
                }
            }

            steps {
                echo 'building the application ...'
                echo "building version ${NEW_VERSION}"
                // sh "mvn install"
            }
        }

        stage("test") {
            when {
                expression {
                    params.executeTest
                }
            }

            steps {
                echo 'testing the application ...'
                
            }
        }

        stage("deploy") {
            steps {
                echo 'deploying the application ...'

                withCredentials([
                    usernamePassword(credentialsId: 'GITHUB-101', usernameVariable: 'USER', passwordVariable: 'PWD')
                ]) {
                    sh "echo ${USER}:${PWD}"
                    sh "curl https://github.com/ -k --user ${USER}:${PWD}"
                }
            }
        }

    }
}