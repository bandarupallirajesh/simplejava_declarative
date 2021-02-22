pipeline {
    agent any
    parameters {
        string(name: 'MAVENGOAL', defaultValue: 'clean package', description: 'it would clean and package the code')
    }
    options {
        buildDiscarder(logRotator(numToKeepStr: '3', artifactNumToKeepStr: '5'))
    }
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
                    echo ${params.MAVENGOAL}
                    export MAVEN_HOME=/opt/maven
                    export PATH=$PATH:$MAVEN_HOME/bin
                    mvn --version
                    mvn "${params.MAVENGOAL}"
                '''
            }
        }
        stage('post build')
        {
            steps {
                junit 'target/surefire-reports/*.xml'
                archiveArtifacts 'target/*.jar'
                stash includes: 'target/*.jar', name: 'samplejava'
                dir('/opt/jars/'){
                    unstash 'samplejava'
                }
            }
        }
    }
    post {
        always {
            mail to: 'bandarupallirajesh3@gmail.com'
            subject: 'Status of pipeline'
            body: 'please check the result'
        }
    }
}

