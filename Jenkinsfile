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
                        sh "sudo helm package --version ${BUILD_NUMBER} helm/tomcat/ "
                        sh "curl -ulohithrajeurs@gmail.com:Lohith@1994 -T tomcat-${BUILD_NUMBER}.tgz \"https://lohith2022.jfrog.io/artifactory/tomcat-repo-helm/tomcat-${BUILD_NUMBER}.tgz\""
                  }
            }
            stage('deploy'){
                 agent { label 'kubernetes' }
                 steps{
                        sh "helm repo add tomcat-repo-helm https://lohith2022.jfrog.io/artifactory/api/helm/tomcat-repo-helm --username lohithrajeurs@gmail.com --password Lohith@1994"
                        sh "helm repo update"
                        sh "helm upgrade --install tomcat tomcat-repo-helm/tomcat --set tag_name=${BUILD_NUMBER} --version ${BUILD_NUMBER}"
                 }
            }
      }
}
