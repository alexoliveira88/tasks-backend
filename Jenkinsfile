pipeline {
    agent any
    stages {
        stage ('Build Backend') {
            steps {
                sh label: '', script: 'mvn clean package -DskipTests=true'
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
