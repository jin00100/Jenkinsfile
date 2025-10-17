pipeline {
    agent any // 指定流水线可以在任何可用的 Jenkins agent 上执行

    stages {
        stage('Build') {
            steps {
                // 打印一条消息，模拟构建过程
                echo 'Building the application...'
                // 在实际项目中，这里会是 mvn clean install, npm install, go build 等命令
            }
        }
        stage('Test') {
            steps {
                // 打印一条消息，模拟测试过程
                echo 'Running tests...'
                // 在实际项目中，这里会是 mvn test, npm test, go test 等命令
            }
        }
        stage('Deploy') {
            steps {
                // 打印一条消息，模拟部署过程
                echo 'Deploying the application...'
                // 在实际项目中，这里会是 scp, docker push, kubectl apply 等命令
            }
        }
    }

    post {
        // post 部分定义了流水线完成后要执行的操作
        always {
            echo 'Pipeline finished.'
        }
        success {
            echo 'Pipeline executed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
