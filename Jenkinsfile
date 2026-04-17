pipeline {
    agent any

    stages {
        stage('Info') {
            steps {
                echo "Build: ${env.BUILD_NUMBER}"
                echo "Galaz: ${env.GIT_BRANCH}"
            }
        }
        stage('Testy') {
            when {
                expression {
                    env.GIT_BRANCH != 'origin/main'
                }
            }
            steps {
                sh 'python3 test_app.py'
            }
        }
        stage('Gotowe') {
            steps {
                echo 'Pipeline zakonczona.'
            }
        }
    }

    post {
        success {
            echo "OK — galaz: ${env.GIT_BRANCH}, build: ${env.BUILD_NUMBER}"
        }
        failure {
            echo "BLAD w buildzie ${env.BUILD_NUMBER} — sprawdz logi."
        }
    }
}
