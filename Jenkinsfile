pipeline {
    agent any 
    tools { 
        maven 'maven'
        nodejs 'NodeJS'
    }
    stages {
        stage ("Clean up"){
            steps {
                deleteDir()
            }
        }
        stage ("Clone repo"){
            steps {
                sh "git clone https://github.com/Naouresss/springboot-angular-mysql-docker-master.git"
            }
        }
        stage ("Generate backend image") {
              steps {
                   dir("springboot-angular-mysql-docker-master/springboot/app"){
                      sh "mvn clean install"
                      sh "docker build -t app ."
                  }                
              }
          }

       stage("Generate front image") {
            steps {
                dir("springboot-angular-mysql-docker-master/angular-app") {
                    // Add any front-end build commands here (e.g., npm install, ng build)
                    // Replace these commands with the actual commands required to build your Angular application
                    sh "npm install"
                    sh "npm run build"
                    sh "sudo docker build -t frontapp ."
                }
            }
        }
        stage ("Run docker compose") {
            steps {
                 dir("springboot-angular-mysql-docker-master"){
                    sh " docker compose up -d"
                }                
            }
        }
    }
}
