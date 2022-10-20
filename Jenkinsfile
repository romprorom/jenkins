/* Requires the Docker Pipeline plugin */
pipeline {
    agent { docker { image 'python:3.10.7-alpine' } }
    environment {
        JEDNA = "1"
        DVA = "2"
    }
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
            echo 'this will run always ${JEDNA}'
        }
        success {
            echo 'this will run if success ${DVA}'
        }
        unstable {
            echo 'tohle by se melo ukazat, pokud bude build nestabilni'
        }
        changed {
            echo 'tohle se ukaze pokud se zmeni stav pipeline'
            echo 'napriklad pokud predtim failovala'
        }
    }
}
