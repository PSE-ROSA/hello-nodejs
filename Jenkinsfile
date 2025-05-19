pipeline {
    agent { 
        // label 'slave' 
        label 'congcong'
    }

    environment {
        // 修正变量名（原图存在笔误，统一为 NODE_VERSION）
        NODE_VERSION = '14.x'
    }

    tools {
        // 修正工具名称大小写，必须与 Jenkins 全局配置完全一致
        nodejs "NodeJs"  // 原图显示为 "NodeJS"（全大写）
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', 
                url: 'https://github.com/PSE-ROSA/hello-nodejs.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                // 修正命令（原图命令不完整）
                sh "node -v"  // 验证 Node.js 版本
                sh "npm -v"   // 验证 npm 版本
                sh 'npm install'
            }
        }

        stage('Build') {
            steps {
                echo 'Building..'
            }
        }

        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }

        stage('Deploy') {
            steps {
                script {
                    try {
                        // 优化部署逻辑（保留日志）
                        sh 'nohup npm start > app.log 2>&1 &'
                        // 归档日志文件（避免被 cleanWs 删除）
                        archiveArtifacts artifacts: 'app.log', allowEmptyArchive: true
                    } catch (Exception e) {
                        echo "Error starting app: ${e}"
                    }
                }
            }
        }

        // 新增健康检查阶段（验证应用是否运行）
        stage('Health Check') {
            steps {
                script {
                    sh 'curl -I http://localhost:3000 || echo "Application not responding"'
                    sh 'ps aux | grep "node" | grep -v grep || echo "No node process found"'
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