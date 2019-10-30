pipeline {
    agent any
    
    stages {
        stage('checking deploy tools and initial clean'){
            steps{
                sh 'mvn --version'
                sh 'java -version'
                sh 'git --version'
                sh 'rm -rf codebase || true'

            }
        }
        stage('pull down code base'){
            steps{
                sh 'git clone https://github.com/joebadmus/LiquorStoreServlet.git codebase'
            }
        }

        stage('compile and test code'){
            steps{
                sh 'cd codebase && mvn clean install'
            }
        }

        stage('Deploy code to App server'){
            steps {
                sh 'rm -rf /tmp/jenkinskey.pem || true'
                sh 'cp /tmp/jenkins_key4.pem /tmp/jenkinskey.pem && chmod 400 /tmp/jenkinskey.pem'
                sh 'ls -la /tmp' 
                sh 'scp -i /tmp/jenkinskey.pem -o StrictHostKeyChecking=no codebase/target/SampleServlet.war ec2-user@ec2-52-208-152-171.eu-west-1.compute.amazonaws.com:/tmp/tomcat/apache-tomcat-8.5.47/webapps'
                echo 'code Deployed'
            }
        }
        
        stage('test code on app server'){
            steps {
                echo 'code tested'
            }
        }
        

        stage('complete'){
            steps {
                echo 'complete'
            }
        }
    }
}