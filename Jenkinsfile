// 在文件顶部引入共享库
@Library('my-shared-lib') _

pipeline {
    agent any

    parameters {
        // 定义一个字符串参数，用于指定部署环境
        string(name: 'DEPLOY_ENV', defaultValue: 'staging', description: 'Deployment environment (staging or production)')
        // 定义一个布尔参数，用于决定是否执行性能测试
        booleanParam(name: 'RUN_PERFORMANCE_TESTS', defaultValue: false, description: 'Run performance tests?')
    }

    stages {
        stage('Build') {
            steps {
                echo "Building the application..."
            }
        }

        // 并行测试阶段
        stage('Parallel Tests') {
            parallel {
                stage('Unit Tests') {
                    steps {
                        echo "Running unit tests..."
                        // 模拟单元测试耗时
                        sh 'sleep 5'
                    }
                }
                stage('Integration Tests') {
                    steps {
                        echo "Running integration tests..."
                        // 模拟集成测试耗时
                        sh 'sleep 10'
                    }
                }
            }
        }

        // 条件执行的性能测试阶段
        stage('Performance Tests') {
            when {
                // 仅当 RUN_PERFORMANCE_TESTS 参数为 true 时执行
                expression { params.RUN_PERFORMANCE_TESTS == true }
            }
            steps {
                echo "Running performance tests..."
            }
        }

        // 条件执行的部署阶段
        stage('Deploy') {
            when {
                // 仅当分支是 main 并且部署环境是 production 时才执行
                branch 'main'
                expression { params.DEPLOY_ENV == 'production' }
            }
            steps {
                echo "Deploying to ${params.DEPLOY_ENV} environment..."
            }
        }
    }

    // 这是被替换和更新后的 post 块
    post {
        always {
            // 调用共享库中的函数
            script {
                pipelineUtils.notify(currentBuild.currentResult)
            }
        }
        success {
            echo 'Pipeline executed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}

