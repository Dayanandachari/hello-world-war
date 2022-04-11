pipeline{
      agent { label 'slave1' }
      environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerpassword')
    }
      stages{
      stage('check out'){
                  steps{
                  sh "rm -rf hello-world-war"
                  sh "git clone https://github.com/Dayanandachari/hello-world-war.git"
                  }
                  }
      stage('build'){
      steps{
      sh "pwd"
      sh "ls"
      sh "cd hello-world-war"
      sh "docker build -t dayanand1991/docker:1.0 ."
      }
      }
       stage('publish'){
                  steps{
                        sh "echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin"
                        sh "docker push dayananda1991/docker:1.0"
                  }
            }
            stage('deploy'){
                  agent { label 'slave1' }
                  steps{
                        sh "docker login -u dayananda1991 -p admin@123"
                        sh "docker pull dayananda1991/docker:1.0"
                       //sh "docker rm -f trail1"
                        sh "docker run -d -p 8085:8080 --name trail1 dayananda1991/docker:1.0"
                  }
            }
      }
    }
