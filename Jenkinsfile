pipeline {
    agent { label slave2 }
    stages {
        stage('checkout') { 
            steps {
              sh "git pull https://github.com/sand1994179/hello-world-war.git"
            }
        }
stage('build') { 
            steps {
              sh "mvn clean package"
            }
        }  
stage('deploy') {
            steps {
                sh " cp /home/slave2/workspace/job_pip/target/hello-world-war-1.0.0.war /opt/apache-tomcat-9.0.60/webapps"
            }
        }
    }
}
