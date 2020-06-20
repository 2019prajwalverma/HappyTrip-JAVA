pipeline{
    agent any
  stages{ 
 
    stage('SCM Checkout'){
        steps{
            checkout([$class: 'GitSCM', branches: [[name: '*/master']], browser: [$class: 'GithubWeb', repoUrl: 'https://github.com/2019prajwalverma/HappyTrip-JAVA.git'], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/2019prajwalverma/HappyTrip-JAVA.git']]])
            }
      
    }
    
    stage('Compile and Create war file'){
         tools { 
                           jdk 'JDK4' 
                           maven 'maven 3.6.3' 
                    } 
        steps{
            dir("happytrip-code/"){
                     //Get maven home path
                //def mvnHome = tool name: 'maven 3.6.3', type: 'maven'
                
                bat label: '', script: 'mvn clean package'
            
            }
            
           
        }
        
    }
    
    stage('Asking to proceed'){
        steps{
            input('Do you want to proceed?')
        }
    }
    
    
    
    stage('Deploy to Tomcat'){
        steps{
             deploy adapters: [tomcat7(credentialsId: '35b3ddb4-0e3e-4d88-a313-caaaa691ed0d', path: '', url: 'http://localhost:8070/')], contextPath: '/happytrip2', war: '**/*.war'
        
                }
       
        }
    }
}
