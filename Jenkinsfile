pipeline {
    agent any
    parameters {
        string(name: 'MAVENGOAL', defaultValue: 'clean package', description: 'it would clean and package the code')
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
		sh "echo ${params.MAVENGOAL}"
                sh '''
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
                junit 'Sample-Declarative/target/surefire-reports/*.xml'
                archiveArtifacts 'Sample-Declarative/target/*.jar'

            }
        }
    }
}
