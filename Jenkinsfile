pipeline {
    agent any
    stages {
        stage ('Build Backend') {
            steps {
                sh label: '', script: '/etc/apache-maven-3.6.3/bin/mvn clean package -DskipTests=true'
            }
        }
        stage ('Meio') {
            steps {
                sh label: '', script: 'echo meio '
            }
        }
        stage ('Fim') {
            steps {
                sleep(5)
                sh label: '', script: 'echo Fim '
            }
        }
    }
    
}
