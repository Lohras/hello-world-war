//CI-CD pipeline for building and deploying
pipeline{
      agent { label 'kubernetes' }
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
      sh "docker build -t lohith1994/dockerrepo:2.0 ."
      }
      }
       stage('publish'){
                  steps{
                        sh "docker login -u lohith1994 -p Lohith@1994"
                        sh "docker push lohith1994/dockerrepo:2.0"
                  }
            }
            stage('deploy'){
                  steps{
                        //sh "docker login -u lohith1994 -p Lohith@1994"
                        //not necessary as it'll refer to docker hub is (default) & repo is public
                        //sh "docker pull lohith1994/dockerrepo:1.0"
                        //sh "docker rm -f docker1"
                        //sh "docker run -d -p 8040:8080 --name docker1 lohith1994/dockerrepo:1.0"
                        sh "sudo su -"
                        sh "echo 'export KUBECONFIG=$HOME/admin.conf' >> $HOME/.bashrc"
                        sh "export KUBECONFIG=/etc/kubernetes/admin.conf"
                        sh "cp /etc/kubernetes/admin.conf $HOME/"
                        //sh "chown root:root $HOME/admin.conf"
                        sh "export KUBECONFIG=$HOME/admin.conf"
                        sh "kubectl apply -f kube.yml"
                  }
            }
      }
      }
