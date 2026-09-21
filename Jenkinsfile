pipeline{
    agent {
        label "node1"
    }
    stages("checkout"){
        steps{
            checkout scm
        } 
    }
    stages("docker build image"){
        steps{
            sh "docker compose build"
        }
    }
    stages("deploy containers"){
        steps{
            sh "docker compose up -d"
        }
    }
    stages("run migrations"){
        steps{
            sh 'docker compose exec -T appseed_app python manage.py migrate'
        }
    }
    stages("verify deployment"){
        steps{
            sh 'docker compose ps'
        }
    }
    post{
        success{
            echo "Deployment completed successfully!"
        }
        failure{
            echo "Deployment failed. Check the Jenkins console output."
        }
    }

}