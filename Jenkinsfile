pipeline {
    agent none

    tools{
        maven "mymaven"
    }
    stages {
        stage('Compile') {
            agent any
            steps {
               script{
                   echo "Compile the Code "
                   sh "mvn compile"
               }
            }
        }
        stage('UnitTest') {
            agent any
            steps {
               script{
                   echo "Unit Test the Code "
                   sh "mvn test"
               }
            }
            post{
                always{
                   junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Package') {
            agent {label 'linux_slave'}
            steps {
               script{
                   echo "Package the Code "
                   sh "mvn package"
               }
            }
        }
    }
}

