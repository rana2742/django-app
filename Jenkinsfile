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
                echo 'deploying the code'
                sh "docker stop notes-app || true"
                sh "docker rm notes-app || true"
                sh "docker run -d -p 8000:8000 --name notes-app rana2742/notes-app:latest python manage.py runserver 0.0.0.0:8000"
            }
        }
    }
}
