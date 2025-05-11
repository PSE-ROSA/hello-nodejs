pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/PSE-ROSA/hello-nodejs.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run App') {
            steps {
                script {
                    try {
                        // 如果之前有运行的 Node 进程，先杀掉
                        sh 'pkill node || true'
                        // 后台运行 Node 应用
                        sh 'nohup node app.js > app.log 2>&1 &'
                    } catch (Exception e) {
                        echo "Error starting app: ${e}"
                    }
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline completed.'
        }
    }
}