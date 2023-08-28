    pipeline {
        agent {
            docker {
                image 'timbru31/node-alpine-git:16' 
                args '-p 3000:3000' 
            }
        }
        environment {
            GITHUB_TOKEN     = credentials('jenkins-github-token')
            GITHUB_REPOSITORY = 'affansholahuddin/a428-cicd-labs'
        }
        stages {
            stage('Build') { 
                steps {
                    sh 'npm install'
                }
            }
            stage('Test') {
                steps {
                    sh './jenkins/scripts/test.sh'
                }
            }
            stage('Deploy') {
                steps {
                    input message: 'Lanjutkan ke tahap Deploy? (Klik "Proceed" untuk melanjutkan eksekusi | Klik "Abort" untuk menghentikan eksekusi)'
                    sh './jenkins/scripts/deliver.sh'
                    sleep(time: 1, unit: 'MINUTES')
                    sh './jenkins/scripts/kill.sh'
                    sh 'chmod +x ./jenkins/scripts/github-pages.sh && ./jenkins/scripts/github-pages.sh'
                }
            }
        }
    }