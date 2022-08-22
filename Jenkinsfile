
import groovy.json.JsonOutput

def COLOR_MAP = [
    'SUCCESS' : 'good',
    'FAILURE' : 'danger'
    ]

def getBuildUser(){
    return currentBuild.rawBuild.getCause(Cause.UserIdCause).getUserId()
    }

slackSend channel: '#gocd-build-notifications',
                      color: '#439FE0',
                      message: "*STARTED:* By *${currentBuild.getBuildCauses()[0].userId}*   *Job_Name:* ${env.JOB_NAME}   *Build_No:* ${env.BUILD_NUMBER}"

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
//             script{
//                 BUILD_USER = getBuildUser()
//             }
              
            slackSend channel: '#gocd-build-notifications',
                      color: COLOR_MAP[currentBuild.currentResult],
                      message: "*${currentBuild.currentResult}:* By *${currentBuild.getBuildCauses()[0].userId}*  *Job_Name:* ${env.JOB_NAME}  *Build_No:* ${env.BUILD_NUMBER} \n More Information At: <${env.BUILD_URL}|Click here>"  
                }
            }
    
}
