pipeline {
    agent any
    tools {
        maven 'maven-3.9.9'
    }
    stages {
        stage("Build") {
            steps {
                script {
                    sh "mvn clean package"
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
                    deploy adapters: [tomcat9(credentialsId: 'tomcatuser', path: '', url: 'http://34.206.202.193:8081/')], contextPath: null, war: '**/*.war'
                }
            }
        }
    }
}
