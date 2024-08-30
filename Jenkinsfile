pipeline {
    agent any
    tools{
    jdk 'jdk17'
    maven 'maven3'
    }
    environment {
        SCANNER_HOME= tool 'sonar-scanner'  
    }
    stages {
        stage('Git checkout') {
            steps {
                git branch: 'main', url: 'git url'
            }
        }
        stage('compile') {
            steps {
                sh 'mvn compile'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Trivy Fs Scan') {
            steps {
                sh "trivy fs --format table -o fs.html ."
            }
        }
        stage('Sonarqube Analysis') {
            steps {
                withSonarQubeEnv('sonar-server') {
                sh '''$SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=blogging-app -Dsonar.projectKey=blogging-app \
                        -Dsonar.java.binaries=target'''
             }
            }
        }
        stage('Build') {
            steps {
                sh 'mvn package'
            }
        }
        stage('publish artifacts') {
            steps {
                withMaven(globalMavenSettingsConfig: 'maven-setting', jdk: 'jdk17', maven: 'maven3', mavenSettingsConfig: '', traceability: true) {
                sh 'mvn deploy'
               }
            }
        }
        stage('Docker Build & Tag') {
            steps {
                script{
                withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                sh 'docker build -t username/bloggingapp:latest .'
                 }
                }
            }
        }    
        stage('Trivy image Scan') {
            steps {
                sh "trivy image --format table -o image.html username/bloggingapp:latest"
            }
        }    
        stage('Docker Push Image') {
            steps {
                script{
                withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                sh 'docker push usename/bloggingapp:latest'
                 }
                }
            }
        }  
    }
}
