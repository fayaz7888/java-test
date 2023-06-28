pipeline {
    agent any

    environment {
        function_name = 'jenkins'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Build'
                sh 'mvn package'
            }
        }

        stage('Push') {
            steps {
                echo 'Push'

                sh "aws s3 cp target/sample-1.0.3.jar s3://jenkinsfayaz"
            }
        }

        stage('Deploy') {
            steps {
                echo 'deploy'

                sh "aws lambda update-function-code --function-name $function_name --region us-east-1 --s3-bucket jenkinsfayaz --s3-key sample-1.0.3.jar"
            }
        }
    }
}
