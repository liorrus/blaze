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
        steps{    
            dir('blaze'){
                sh 'sed -i \'s/{build}/$BUILD_NUMBER/g\' index.html'
                sh 'docker rmi liorruslander/blaze:v2 '
                sh 'docker build -t liorruslander/blaze:v2 .'
                sh 'docker push liorruslander/blaze:v2'

            }
        }
        }
        stage('pull') {
            steps {
                sh 'docker pull nginx'
            }
        }
    }
}
