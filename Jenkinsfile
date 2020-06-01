pipeline {
    agent any
    stages {
        stage ('inicio') {
            steps {
                sh label: '', script: 'echo inicio '
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
