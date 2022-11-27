pipeline{
    agent any
    tools {
        maven 'myMaven'
    }
    stages{
        stage("Code Checkout"){
            steps{
                echo "========Code Checkout========"
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'myGitCredentials', url: 'https://github.com/gthborg/hello-world-war.git']]])
            }
            post{
                always{
                    echo "========always========"
                }
                success{
                    echo "========A executed successfully========"
                }
                failure{
                    echo "========A execution failed========"
                }
            }
        }
        stage("Build"){
            steps{
                echo "========build========"
                sh 'mvn -s settings.xml clean install deploy '
            }
            post{
                always{
                    echo "========always========"
                }
                success{
                    echo "========A executed successfully========"
                    archiveArtifacts artifacts: 'target/*.war', followSymlinks: false
                    build 'Hello-world-Deployment-pipeline'
                }
                failure{
                    echo "========A execution failed========"
                }
            }
        }
    }
    post{
        always{
            echo "========always========"
        }
        success{
            echo "========pipeline executed successfully ========"
        }
        failure{
            echo "========pipeline execution failed========"
        }
    }
}