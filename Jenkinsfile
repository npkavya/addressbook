pipeline {
    agent none

    tools{
        maven "mymaven"
    }
    environment{
        BUILD_SERVER='ec2-user@172.31.13.81'
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
        stage('UnitTest') { //running on slave1
            agent {label 'linux_slave'}
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
        stage('Package') { //running on slave2 via ssh-agent
            agent any
            steps {
               script{
                    sshagent(['Slave2']) {
                    echo "Package the Code "
                    
                    sh "scp -o StrictHostKeyChecking=no server-config.sh ${BUILD_SERVER}:/home/ec2-user"
                    sh "ssh -o StrictHostKeyChecking=no ${BUILD_SERVER} 'bash server-config.sh'"
                    }
                }
            }
        }
    }
}

