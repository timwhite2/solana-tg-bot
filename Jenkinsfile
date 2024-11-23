pipeline {
    agent {
        dockerContainer {
            image 'rust:latest'
        }
    }
    environment {
        CARGO_HOME = "${WORKSPACE}/.cargo"
    }
    stages {
        stage('Checkout') {
            steps {
                branches: [[name: '*/main']],
                userRemoteConfigs: [[
                url: 'git@github.com:timwhite2/solana-tg-bot.git',
                credentialsId: '1'
                ]]])
            }
        }
        stage('Setup') {
            steps {
                sh '''
                rustup update
                cargo update
                '''
            }
        }
        stage('Build') {
            steps {
                sh 'cargo build --release'
            }
        }
        stage('Test') {
            steps {
                sh 'cargo test'
            }
        }
        stage('Run') {
            steps {
                sh 'cargo run --release'
            }
        }
    }
    post {
        always {
            sh 'cargo clean'
        }
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
