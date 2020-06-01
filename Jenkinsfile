pipeline {
    agent any
    stages {
        stage ('Build Backend') {
            steps {
                sh label: '', script: '/etc/apache-maven-3.6.3/bin/mvn clean package -DskipTests=true'
            }
        }
        stage ('Unit Tests') {
            steps {
                sh label: '', script: '/etc/apache-maven-3.6.3/bin/mvn test'
            }
        }

    }
    
}
