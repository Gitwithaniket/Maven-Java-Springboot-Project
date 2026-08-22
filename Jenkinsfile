pipeline {

    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Environment Check') {
            steps {
                sh '''
                    echo "===== JAVA ====="
                    java -version

                    echo "===== MAVEN ====="
                    mvn -version

                    echo "===== DOCKER ====="
                    docker --version

                    echo "===== DOCKER COMPOSE ====="
                    docker-compose version

                    echo "===== WORKSPACE ====="
                    pwd

                    echo "===== FILES ====="
                    ls -la
                '''
            }
        }

        stage('Maven Build') {
            steps {
                dir('backend') {
                    sh '''
                        mvn clean package -DskipTests
                    '''
                }
            }
        }
    }

    post {
        success {
            echo '================================='
            echo 'JENKINS BUILD SUCCESSFUL'
            echo '================================='
        }

        failure {
            echo '================================='
            echo 'JENKINS BUILD FAILED'
            echo '================================='
        }
    }
}
