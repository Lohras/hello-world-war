//CI-CD pipeline for building and deploying
// prequisites: jenkins up and running with 2 slaves : 1) docker-slave (docker/awscli/java should be installed in slave) 
// 2) k8s-master slave ( in k8s, add user and run the commandsto give permission of folder .kube) 
pipeline{
      agent { label 'java' }
      stages{
            stage('check out'){
                  steps{
                        sh "rm -rf hello-world-war"
                        sh "git clone https://github.com/Lohras/hello-world-war.git"
                  }
            }
            stage('build'){
                  steps{
                        sh "pwd"
                        sh "ls"
                        sh "cd hello-world-war"
                        sh "echo ${BUILD_NUMBER}"
                        sh "docker build -t 127801862567.dkr.ecr.us-east-1.amazonaws.com/tomcat:${BUILD_NUMBER} ."
                  }
            }
            stage('publish'){
                  steps{
                        sh "aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 127801862567.dkr.ecr.us-east-1.amazonaws.com"
                        sh "docker push 127801862567.dkr.ecr.us-east-1.amazonaws.com/tomcat:${BUILD_NUMBER}"
                        sh "pwd"
                        sh "ls"
                        sh "sudo helm package --version ${BUILD_NUMBER} -d helm/tomcat . "
                        sh "curl -ulohithrajeurs@gmail.com:Lohith@1994 -T tomcat-${BUILD_NUMBER}.tgz \"https://lohith2022.jfrog.io/artifactory/tomcat-repo-helm/tomcat-${BUILD_NUMBER}.tgz\""
                  }
            }
            // stage('deploy'){
               //   agent { label 'slave2' }
                 // steps{
                        //sh "docker login -u lohith1994 -p Lohith@1994"
                        //not necessary as it'll refer to docker hub is (default) & repo is public
                   //     sh "docker pull lohith1994/dockerrepo:1.0"
                     //   sh "docker rm -f docker1"
                       // sh "docker run -d -p 8040:8080 --name docker1 lohith1994/dockerrepo:1.0"
                 // }
           // }
      }
      }
