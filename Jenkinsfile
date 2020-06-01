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
                sleep(20) 
                timeout(time: 1, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
        stage ('Deploy backend') {
            steps {
                deploy adapters: [tomcat8(credentialsId: 'TomcatLogin', path: '', url: 'http://10.33.7.232:8001/')], contextPath: 'tasks-backend', war: '**/tasks-backend.war'
            }
        }
        stage ('Api Test') {
            steps {
                dir('api-test') {
                    git credentialsId: '0813905c-10c6-4966-9f1b-df87a61ba293', url: 'https://github.com/alexoliveira88/tasks-api-test'
                    sh label: '', script: '/etc/apache-maven-3.6.3/bin/mvn test'
                }
            }
        }
        stage ('Deploy Frontend') {
            steps {
                dir('frontend') {
                    git credentialsId: '0813905c-10c6-4966-9f1b-df87a61ba293', url: 'https://github.com/alexoliveira88/tasks-frontend'
                    sh label: '', script: '/etc/apache-maven-3.6.3/bin/mvn clean package'
                    deploy adapters: [tomcat8(credentialsId: 'TomcatLogin', path: '', url: 'http://10.33.7.232:8001/')], contextPath: 'tasks', war: '**/tasks.war'
            }
        }
    }
    
}

