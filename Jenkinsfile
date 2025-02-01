pipeline{
    agent any
    environment{
        APP_DEST_PATH = "/var/www/${env.APP_FOLDER_NAME}"
        APP_DEST_PATH_CHECK = fileExists "${env.APP_DEST_PATH}"
    }
    stages{
        stage("Fetch code from git"){
            steps{
                git branch: 'main', url: 'https://github.com/Krukru102999/abi-vday-2025.git'
            }
        }
        stage("Unit test"){
            steps{
                sh "echo 'Unit test'"
            }
        }
        stage("Setting up Environment") {
            when { expression { APP_DEST_PATH_CHECK == "true"} }
            steps {
                sh "sudo rm -R ${env.APP_DEST_PATH}"
                sh "pwd"
            }
        }
        stage("Build"){
            steps{
                sh "npm run build"
            }
            post{
                always{
                    echo "Done building"
                }
                success{
                    echo "========Building success!========"
                }
                failure{
                    echo "========A execution failed========"
                }
            }
        }
        stage("Deployment"){
            steps{
                sh "sudo cp -R . ${env.APP_DEST_PATH}"
            }
            post{
                always{
                    echo "Done building"
                }
                success{
                    echo "========Building success!========"
                }
                failure{
                    echo "========A execution failed========"
                }
            }
        }
    }
    post{
        success{
            echo "========pipeline executed successfully ========"
        }
        failure{
            echo "========pipeline execution failed========"
        }
    }
}