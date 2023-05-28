pipeline{
    
    agent any 
    
    stages {
        
        stage('Git Checkout'){
            
            steps{
                
                script{
                    
                    git branch: 'main', url: 'https://github.com/hegdesandesh25/demo-counter-app.git'
                }
            }
        }
        stage('UNIT testing'){
            
            steps{
                
                script{
                    
                    bat "mvn test"
                }
            }
        }
        stage('Integration testing'){
            
            steps{
                
                script{
                    
                    bat "mvn verify -DskipUnitTests"
                }
            }
        }
        stage('Maven build'){
            
            steps{
                
                script{
                    
                    bat "mvn clean install"
                }
            }
        }
        stage('Static code analysis'){ 
            try{
                  script{
                                          
                        bat "mvn clean package sonar:sonar  -Dsonar.projectKey=demo-counter-app -Dsonar.projectName='demo-counter-app' -Dsonar.login=%sonar-token%"
                    
                   }
                    
                

    } catch(e) {
        build_ok = false
        echo e.toString()  
    }
        }
      /*  stage('Static code analysis'){
            
            steps{
                
                script{
                                          
                        bat "mvn clean package sonar:sonar  -Dsonar.projectKey=demo-counter-app -Dsonar.projectName='demo-counter-app' -Dsonar.login=%sonar-token%"
                    
                   }
                    
                }
            }*/
            stage('Quality Gate Status'){
                
                steps{
                    
                    script{
                        
                        waitForQualityGate abortPipeline: false, credentialsId: 'sonar-token'
                    }
                }
            }
        }
        
}
