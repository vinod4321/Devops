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
                    deploy adapters: [tomcat9(credentialsId: 'tomcatcreds', path: '', url: 'http://3.82.37.105:8081/')], contextPath: null, war: '**/*.war'
                }
            }
        }
    }
}
