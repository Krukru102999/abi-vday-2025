pipeline{
    agent any
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
        stage("Build"){
            steps{
                sh "npm run dev"
            }
            post{
                always{
                    echo "Done building"
                }
                success{
                    sh "npm run start"
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