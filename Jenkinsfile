pipeline {
    agent {
        docker {
            image 'rust:latest'
        }
    }
    environment {
        CARGO_HOME = "${WORKSPACE}/.cargo"
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
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
