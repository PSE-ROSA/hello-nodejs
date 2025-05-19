pipeline {
    agent { 
        label 'slave' // 指定在标签为 slave 的节点上运行
    }

    environment {
        // 设置 Node.js 版本，假设你已经在 Jenkins 中配置好了 NodeJS 插件和版本
        NODE_VERSION = '14.x'
    }

    tools {
    nodejs "NodeJS-14.x"  // 与全局工具配置的名称一致
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/PSE-ROSA/hello-nodejs.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh "node -v"
                sh "npm -v"
                sh 'npm install'
            }
        }

        stage('Build') {
            steps {
                echo 'Building..'
                // 如果有构建步骤，可以在这里添加
            }
        }

        stage('Test') {
            steps {
                echo 'Testing..'
                // 如果有测试命令，可以在这里执行
            }
        }

        stage('Deploy') {
            steps {
                script {
                    try {
                        // 假设你想在 Jenkins 执行环境中运行应用
                        sh 'nohup npm start > app.log 2>&1 &'
                    } catch (Exception e) {
                        echo "Error starting app: ${e}"
                    }
                }
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}