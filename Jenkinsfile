pipeline {
    agent any
    stages{
        stage('Git clone'){
            steps{
              git branch: 'master', url: 'https://github.com/Gautirockz/php-project.git
               }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t saigowtham2605/akshatnewimg6july:v1 .'
                    sh 'docker images'
                }
            }
        }
          stage('Docker login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-pwd', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                    sh "echo $PASS | docker login -u $USER --password-stdin"
                    sh 'docker push saigowtham2605/akshatnewimg6july:v1'
                }
            }
        }
        
     stage('Deploy') {
            steps {
               script {
                   def dockerrm = 'sudo docker rm -f My-first-containe2211 || true'
                    def dockerCmd = 'sudo docker run -itd --name My-first-containe2211 -p 8083:80 akshu20791/akshatnewimg6july:v1'
                    sshagent(['sshkeypair']) {
                        //chnage the private ip in below code
                        // sh "docker run -itd --name My-first-containe2111 -p 8083:80 saigowtham2605/2febimg:v1"
                         sh "ssh -o StrictHostKeyChecking=no ubuntu@172.31.21.192 ${dockerrm}"
                         sh "ssh -o StrictHostKeyChecking=no ubuntu@172.31.21.192 ${dockerCmd}"
                    }
                }
            }
        }
    }
}
