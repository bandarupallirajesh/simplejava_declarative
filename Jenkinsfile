pipeline {
    agent any
    triggers{
        cron(* * * * *)
    }
    parameters {
        string(name: 'mavengoal', defaultValue: 'clean package', description: 'it would clean and package the code')
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
                    export MAVEN_HOME=/opt/maven
                    export PATH=$PATH:$MAVEN_HOME/bin
                    mvn --version
                    mvn ${params.mavengoal}"
                '''
            }
        }
        stage('post build')
        {
            steps {
                junit 'Sample-Declarative/target/surefire-reports/*.xml'
                archiveArtifacts 'Sample-Declarative/target/*.jar'

            }
        }
    }
}
