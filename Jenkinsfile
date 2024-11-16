pipeline {
    agent any
    
    tools
    
    {
        jdk 'jdk18'
        maven 'Maven'
    }

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', changelog: false, credentialsId: 'f37fd0e3-32d8-4ea1-a0e8-f4df6ef31f5c', poll: false, url: 'https://github.com/SRIJANI181/Shopping-Cart.git'
            }
        }
        
         stage('Compile') {
            steps {
                bat "mvn clean compile"
            }
        }
        stage('Build') {
            steps {
                bat "mvn clean package"
            }
        }
        stage('Docker Build & Push') {
            steps {
               script{
                 withDockerRegistry(credentialsId: 'c64dfa1f-90de-4a69-9583-ed92d2a8bd8f') {
                       bat "docker build -t shopping-cart -f docker/Dockerfile ."
                       bat "docker tag shopping-cart srijani2808/shopping-cart:latest"
                       bat "docker push srijani2808/shopping-cart:latest"

                }
               }
            }
        }
        
        // stage('OWASP Scan') {
        //     steps {
        //       dependencyCheck additionalArguments: '--scan ./ ', odcInstallation: 'DP'
        //       dependencyCheckPublisher pattern: '**/dependency-check-report.xml'
               
        //     }
        // }
    }
}
