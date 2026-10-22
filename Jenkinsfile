
pipeline {
    agent any

    parameters {
        booleanParam(
            name: 'RUN_APP',
            defaultValue: true,
            description: 'Run the calculator application'
        )
    }

    stages {
        stage('Compile') {
            steps {
                bat 'mvn compile'
            }
        }

        stage('Test') {
            steps {
                bat 'mvn test'
            }
        }

        stage('Package') {
            steps {
                bat 'mvn package'
            }
        }

        stage('Run') {
            when {
                expression {
                    params.RUN_APP
                }
            }
            steps {
                bat 'java -jar target\\calculator-ci-1.0-SNAPSHOT.jar'
            }
        }
    }

    post {
        always {
            junit 'target/surefire-reports/*.xml'
            archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
        }
    }
}
