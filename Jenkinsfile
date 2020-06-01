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
        stage ('Sonar Analysis') {
            environment {
                scannerHome = tool 'SONAR_SCANNER'
            }
            steps {
                withSonarQubeEnv('SONAR_LOCAL') {
                    sh label: '', script: "${scannerHome}/bin/sonar-scanner -e -Dsonar.projectKey=DeployBack -Dsonar.host.url=http://10.33.7.232:9000 -Dsonar.login=811003a3ef27dd23959dc398d83341734ec17045 -Dsonar.java.binaries=target -Dsonar.coverage.exclusions=**/mvn/**,**/src/test/**,**/model/**,**Application.java"
                }
            } 
        }
        stage ('Quality Gate') {
            steps {
                sleep(30) 
                timeout(time: 1, unit: 'MINUTES')
                    waitForQualityGate abortPipeline: true
            }
        }

    }
    
}
