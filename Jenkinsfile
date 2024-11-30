pipeline {
    agent any

    stages {
        stage('Source') {
            steps {
                git 'https://github.com/horaciokar/unir-cicd.git'
            }
        }

        stage('Build') {
            steps {
                echo 'Building stage!'
                sh 'make build'
            }
        }

        stage('Unit tests') {
            steps {
                sh 'make test-unit'
                archiveArtifacts artifacts: 'results/*.xml'
            }
        }

        stage('Unit tests-api') {
            steps {
                sh 'make test-api'
                archiveArtifacts artifacts: 'results/*.xml'
            }
        }
    }

    post {
        always {
            echo 'Pipeline success.'
            junit 'results/*_result.xml'
            cleanWs()
        }

        failure {
            echo "pipeline failure."
            echo "Job name: ${env.JOB_NAME}"
            echo "Execution number: ${env.BUILD_NUMBER}"
            echo "logs view: ${env.BUILD_URL}"
        }
    }
}
