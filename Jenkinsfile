pipeline{
    agent any
    tools {
        maven "maven3.8.6"
    }
    stages {
        stage('1GetCode'){
            steps{
                bat "echo  'cloning the latest application version' "
                git credentialsId: 'bfead37d-3a80-486f-9bbf-7533424f1e9a', url: 'https://github.com/FutureTechn/maven-web-application-jenk'
            }
            
        }
        stage('2Built&Test'){
            steps{
                bat "echo 'Running Junit testing' "
                bat "echo  'Testing must pass before continue' "
                bat "mvn clean package"
            }
        }
        stage('3codeQuality'){
            steps{
                bat "echo ‘Performing Code Quality’ "
                bat "mvn sonar:sonar"
            }
        }
        stage('4UploadNexus'){
            steps{
                bat "mvn deploy"
            }
        }
        stage('5deploy2UAT'){
            steps{
                bat "echo 'Upload artifact to UAT' "
                deploy adapters: [tomcat9(credentialsId: 'Tomcat-Window', path: '', url: 'http://localhost:8080/')], contextPath: null, war: 'target\\*war'
            }
        }
        
    }
    post{
        always{
            emailext body: '''Please check the results ''', recipientProviders: [buildUser(), requestor(), developers()], subject: 'Success', to: 'bao@gmail.com'
        }
        success{
                emailext body: '''Hey guys Good Morning ''', recipientProviders: [buildUser(), requestor(), developers()], subject: 'Success', to: 'bao@gmail.com'
        }
        failure{
            emailext body: '''Hey guys Good Morning fix the issue and let me know ''', recipientProviders: [buildUser(), requestor(), developers()], subject: 'Success', to: 'bao@gmail.com'
        } 
    }
}
   
