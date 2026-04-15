pipeline {
    agent any
    
    environment {
        LANG = 'en_US.UTF-8'
        LC_ALL = 'en_US.UTF-8'
    }

    tools {
        maven 'Maven'
    }

    stages {

        // ❌ Removed manual checkout (Jenkins already does it)

        stage('Build') {
            steps {
                dir('MyMavenWebApp') {
                    sh 'mvn clean package'
                }
            }
        }

        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'MyMavenWebApp/target/*.war', fingerprint: true
            }
        }

        stage('Deploy') {
            steps {
                dir('MyMavenWebApp') {
                    sh 'ansible-playbook ../ansible/playbook.yml -i ../ansible/hosts.ini'
                }
            }
        }
    }
}
stage('Debug') {
    steps {
        sh 'pwd'
        sh 'ls -R'
    }
}
