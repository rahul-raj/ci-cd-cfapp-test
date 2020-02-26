pipeline {

    agent any

    stages {

        stage ('Build') {
            steps {
                withMaven(maven: 'maven_3_6_3') {
                    sh 'mvn clean package'
                }
            }
        }

        stage ('Deploy') {
            steps {

                withCredentials([[$class          : 'UsernamePasswordMultiBinding',
                                  credentialsId   : 'CloudFoundry-Credentials',
                                  usernameVariable: 'USERNAME',
                                  passwordVariable: 'PASSWORD']]) {

                    sh 'C:/Program Files/Git/bin/cf login -a http://api.run.pivotal.io -u $USERNAME -p $PASSWORD'
                    sh 'C:/Program Files/Git/bin/cf push'
                }
            }

        }

    }

}