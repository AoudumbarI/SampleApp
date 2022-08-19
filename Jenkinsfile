
import groovy.json.JsonOutput

def COLOR_MAP = [
    'SUCCESS' : 'good',
    'FAILURE' : 'danger',
    'STARTED' :  '#439FE0'
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
                      color: '#439FE0',
                      message: "*Started:* By ${BUILD_USER} \n *Job_Name:* ${env.JOB_NAME} \n *Build_No:* ${env.BUILD_NUMBER}"
  
            slackSend channel: '#gocd-build-notifications',
                      color: COLOR_MAP[currentBuild.currentResult],
                      message: "*${currentBuild.currentResult}:* By ${BUILD_USER} \n Job_Name: ${env.JOB_NAME} \n Build_No: ${env.BUILD_NUMBER} \n More Information At: ${env.BUILD_URL}"  
                }
            }
    
}
