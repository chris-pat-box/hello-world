pipeline {
    agent any
    tools {
        maven 'maven'
    }
    stages {
        stage('Checkout'){
            steps {
                echo "inside checkout step"
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'github', url: 'https://github.com/chris-pat-box/hello-world.git']]]) 
            }
        }
        stage('Build'){
            steps{
                echo "inside build step"
                sh 'mvn clean install package -f pom.xml'
            }
        }
        stage('Deploy'){
            steps{
                echo "inside deployment step"
                deploy adapters: [tomcat9(credentialsId: 'Tomcat_Credentials', path: '', url: 'http://localhost:8090/')], contextPath: null, war: '**/*.war'
            }
        }
        stage('Custom Stage'){
            steps{
                echo " Job name is - ${env.JOB_NAME}\n Build number is - ${env.BUILD_NUMBER}\n Build URL is - ${env.BUILD_URL}\n Build ID is - ${env.BUILD_ID}"
                echo " Branch name is - ${env.BRANCH_NAME}\n Build Path is - ${env.PATH}\n Workspace Path - ${env.WORKSPACE}" 
            }
        }
    }
}
