  @Library('shared') _
pipeline {
    agent { label "ubuntu-ec2-agent" }

    stages {

        stage('shared library') {
            steps {
                script {
                    hello()
                }
            }
        }

        stage('code') {
            steps {
               script{
                clone( "https://github.com/rana2742/django-app.git","main")
              }
            }
        }

        stage('build') {
            steps {
                script{
                    build("notes-app","latest","rana2742")
                }
            }
        }

        stage('push') {
            steps {
                script{
                        push("notes-app","latest","rana2742")
                }
            }
        }
 stage('deploy') {
    steps {
        echo 'This is deployment area'
        sh """
            docker-compose down || true
            docker-compose up -d --build
        """
    }
}

    }
}
