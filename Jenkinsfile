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
        stage('Uruchom aplikacje') {
            steps {
                sh '''
                    pkill -f "python3 app.py" || true
                    nohup python3 app.py > app.log 2>&1 &
                    sleep 3
                    curl -sf http://localhost:5000/ > /dev/null
                    echo "Aplikacja dziala na porcie 5000"
                '''
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
