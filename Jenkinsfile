
pipeline {
    agent { docker { image 'maven:3.3.3' } }
    stages {
        stage('build') {
            steps {
                sh 'echo hello world'
                sh 'mvn --version'
                sh 'echo Bye bye'
            }
        }
    }
}
