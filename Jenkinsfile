pipeline {
    agent any

    tools{
        maven "mymaven"
    }
    stages {
        stage('Compile') {
            steps {
               script{
                   echo "Compile the Code "
                   sh "mvn compile"
               }
            }
        }
        stage('UnitTest') {
            steps {
               script{
                   echo "Unit Test the Code "
                   sh "mvn test"
               }
            }
        }
        stage('Package') {
            steps {
               script{
                   echo "Package the Code "
                   sh "mvn package"
               }
            }
        }
    }
}

