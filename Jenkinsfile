pipeline {
    agent any
    tools {
        maven 'maven-3.9.6'
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
i
        stage('Deploy to Tomcat Server') {
            steps {
                script {
                    deploy adapters: [tomcat9(credentialsId: 'tomcatcreds', path: '/opt/apache-tomcat-9.0.96/webapps/', url: 'http://43.205.216.229:8082/'], contextPath: null, war: '**/*.war'
                }
            }
        }
    }
}
