pipeline {
    agent any
    stages {

        // Primeiro stage
        stage('Sync GitHub Backend') {
            steps {
                dir('backend'){
                    git credentialsId: 'GitHub', url: 'git@github.com:leandrotech/tasks-backend.git'
                }      
            }
        }

        // Segundo stage
        stage('Build Backend') {
            steps {
                sh 'cd backend && mvn clean package'    
            }
        }

        // Terceiro stage
        stage('Testes Unitários') {
            steps {
                sh 'cd backend && mvn test'    
            }
        }

        // Quarto stage
        stage('Deploy Backend'){
            steps{            
                deploy adapters: [tomcat8(credentialsId: 'tomcat-access', path: '', url: 'http://54.210.20.88:8080')], contextPath: 'tasks-backend', war: 'backend/target/tasks-backend.war'                
            }                        
            
        }      

        // Quinto stage  
        stage('Sync GitHub Frontend'){
            steps{  
                dir('frontend'){
                git credentialsId: 'GitHub', url: 'git@github.com:leandrotech/tasks-frontend.git'              
                }
            }              
        }

        // Sexto stage
        stage('Build Frontend') {
            steps {
                sh 'cd frontend && mvn clean package'    
            }
        }

        // Sétivo stage
        stage('Deploy Frontend'){
            steps{            
                deploy adapters: [tomcat8(credentialsId: 'tomcat-access', path: '', url: 'http://54.210.20.88:8080')], contextPath: 'tasks', war: 'frontend/target/tasks.war'                
            }                        
            
        }

        // Oitavo stage
        stage('Teste Funcional'){
            steps{
                sh 'echo Aqui vai o teste funcional'            
            }                        
            
        }
    }

    // Ação de pós build
    post {
        success{
            sh 'echo @@@@TUDO OK!@@@@'
        } 
        unsuccessful{
            sh 'echo @@@@ERRO GRAVE!@@@@'
        }
        fixed{
            sh 'echo @@@@VOLTOU A FUNCIONAR!@@@@'
        }               
    }
}   