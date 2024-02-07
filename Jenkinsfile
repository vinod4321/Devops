pipeline {
    agent any

    stages {
        stage("Build") {
            steps {
                script {
                    sh "clean package"
                }
            }
            post {
                success {
                    echo "Archiving the Artifacts"
                    archiveArtifacts artifacts: "**/target/*.war"
                }
            }
        }

        stage('Deploy to Tomcat Server') {
            steps {
                script {
                    deploy adapters: [tomcat9(credentialsId: 'tomat1', path: '', url: 'http://43.204.120.90:8082/')], contextPath: null, war: '**/*.war'
                }
            }
        }
    }
}
