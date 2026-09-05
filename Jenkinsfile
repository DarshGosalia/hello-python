pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                url: 'https://github.com/DarshGosalia/hello-python.git'
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
                    -Dsonar.login=squ_e9ae0a11e21b5c43bb053c5229ad7223ba4cb6f0
                    '''
                }
            }
        }
    }
}
