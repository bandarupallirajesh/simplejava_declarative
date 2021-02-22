pipeline {
    agent any
    stages {
        stage('scm pull')
        {
            steps {
                git 'https://github.com/jenkins-docs/simple-java-maven-app.git'
            }
        }
        stage('build')
        {
            steps {
                sh '''
                    export MAVEN_HOME=/opt/maven
                    export PATH=$PATH:$MAVEN_HOME/bin
                    mvn --version
                    mvn clean package
                '''
            }
        }
        stage('post build')
        {
            steps {
                junit 'target/surefire-reports/*.xml'
                archiveArtifacts 'target/*.jar'

            }
        }
    }
}
