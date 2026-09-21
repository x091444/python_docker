pipeline{
    agent {
        label "node1"
    }

    stages{
        stage("checkout"){
            steps{
                checkout scm
            }
        }

        stage("copy .env file"){
            steps{
                sh 'cp /home/ubuntu/python_docker/.env .env'
            }

        }

        stage("docker build image"){
            steps{
                sh "docker compose build"
            }
        }

        stage("deploy containers"){
            steps{
                sh "docker compose up -d"
            }
        }

        stage("run migrations"){
            steps{
                sh 'docker compose exec -T appseed_app python manage.py migrate'
            }
        }

        stage("verify deployment"){
            steps{
                sh 'docker compose ps'
            }
        }
    }
    post{
        success{
            echo "Deployment completed successfully."
        }
        failure{
            echo "Deployment failed. Check the Jenkins console output."
        }
    }
}
