pipeline {
    agent none

    stages {
        stage('build') {
            agent {
                label 'buildnode'
            }
            steps {
                deleteDir()

                sh '''
                    git clone https://github.com/Anuragh-git/webserver.git
                    ls -la
                '''

                stash name: 'webpage', includes: 'webserver/**'
            }
        }

        stage('deploy') {
            agent {
                label 'deploy'
            }
            steps {
                deleteDir()

                unstash 'webpage'

                sh '''
                    rm -rf /var/www/html/*
                    cp -r webserver/* /var/www/html/
                    ls -la /var/www/html/
                '''
            }
        }
    }
}
