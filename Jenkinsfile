/* Requires the Docker Pipeline plugin */
pipeline {
    agent { docker { image 'python:3.10.7-alpine' } }
    stages {
        stage('build') {
            steps {
                sh 'python --version'
                sh 'python --version'
                sh '''
                    echo "ahoj"
                    echo "dalsi radek"
                    ls -lah
                '''
            }
        }
        stage('deploy') {
            steps {
                retry(2) {
                    sh './flakey-deploy.sh'
                }
                timeout(time: 3, unit: 'MINUTES') {
                    sh './health.sh'
                }
            }
        }
    }
    post {
        always {
            echo 'this will run'
        }
        success {
            echo 'this will run if success'
        }
        changed {
            echo 'tohle se ukaze pokud se pipeline zmeni'
            echo 'zkusit pridat unstable'
        }
    }
}
