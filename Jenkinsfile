pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git 'https://github.com/DarshGosalia/hello-python.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'pip3 install -r requirements.txt'
            }
        }

        stage('Test') {
            steps {
                sh 'pytest'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonarqube') {
                    sh '''
                    sonar-scanner \
                    -Dsonar.projectKey=hello-python \
                    -Dsonar.sources=. \
                    -Dsonar.host.url=http://http://13.232.5.163/:9000 \
                    -Dsonar.login=$SONAR_AUTH_TOKEN
                    '''
                }
            }
        }
    }
}
