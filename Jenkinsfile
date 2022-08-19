
import groovy.json.JsonOutput

def COLOR_MAP = [
    'SUCCESS' : 'good',
    'FAILURE' : 'danger',
    'STARTED' :  '#00FF00'
    ]

def getBuildUser(){
    return currentBuild.rawBuild.getCause(Cause.UserIdCause).getUserId()
    }

pipeline {
    agent any
    environment{
      BUILD_USER = ''
  }
    stages {
        stage('Hello') {
            steps {
                echo "Hello world"
                    }
            }
        }
    post{
        always{
            script{
                BUILD_USER = getBuildUser()
            }
            slackSend channel: '#gocd-build-notifications',
                      color: COLOR_MAP[currentBuild.currentResult],
                      message: "Started:  \n by ${BUILD_USER} \n *${currentBuild.currentResult}:* ${env.JOB_NAME} build ${env.BUILD_NUMBER} \n More Information At: ${env.BUILD_URL}"        }
            }
    
}
