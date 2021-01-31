pipeline {
    agent any
    stages {
        stage('clear-workspace'){
            steps{
                sh 'rm -rf blaze'
            }
        }
        stage('clone'){
            steps{
                sh 'git clone  https://github.com/liorrus/blaze.git'
            }
        }
        stage ('blaze'){
            environment {
            BUILD_NUMBER = "${env.BUILD_NUMBER}"
                
            }
            steps{    
                dir('blaze'){
                    sh 'sed -i \'s/{build}/$BUILD_NUMBER/g\' index.html'
                    sh 'docker rmi liorruslander/blaze:v2 '
                    sh 'docker build -t liorruslander/blaze:v2 .'
        
                    sh 'docker push liorruslander/blaze:v2'

                }
            }
        }
        stage('deploy k8s') {
            steps {
                sh '/var/jenkins_home/kubectl/kubectl  --kubeconfig /var/jenkins_home/kubectl/config delete pods `/var/jenkins_home/kubectl/kubectl  --kubeconfig /var/jenkins_home/kubectl/config get pods | cut -f 1 -d \' \' | grep nginx-dep`'
            }
        }
    }
}
