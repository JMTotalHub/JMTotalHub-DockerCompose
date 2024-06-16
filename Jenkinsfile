pipeline {
    agent {
        docker {
            image 'docker:latest'
            args '-v /var/run/docker.sock:/var/run/docker.sock'
        }
    }

    environment {
        DATABASE_URL = credentials('DATABASE_URL')
        REACT_APP_ENV = credentials('REACT_APP_ENV')
        REACT_APP_SERVER_IP = credentials('REACT_APP_SERVER_IP')
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/JMTotalHub/JMTotalHub-DockerCompose.git', branch: 'main'
            }
        }

        stage('Build and Deploy') {
            steps {
                script {
                    // 도커 컴포즈 파일 실행
                    sh 'docker-compose -f docker-compose.yml pull'
                    sh 'docker-compose -f docker-compose.yml up -d --force-recreate'
                }
            }
        }
    }
}
