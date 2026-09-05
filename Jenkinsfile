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
                sh '''
                python3 -m venv venv
                . venv/bin/activate
                pip install --upgrade pip
                pip install -r requirements.txt
                '''
            }
        }

        stage('Test') {
            steps {
                sh '''
                . venv/bin/activate
                pytest
                '''
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonarqube') {
                    sh '''
                    . venv/bin/activate

                    sonar-scanner \
                    -Dsonar.projectKey=hello-python \
                    -Dsonar.projectName=hello-python \
                    -Dsonar.sources=. \
                    -Dsonar.host.url=http://13.232.5.163:9000
                    '''
                }
            }
        }
    }
}
