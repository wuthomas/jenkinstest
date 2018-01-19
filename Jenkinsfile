node {

  stage 'checkout project'
  checkout scm

  stage 'check env'

  echo "Set env vars"
  echo "Print env vars"
  sh 'printenv'

	
pipeline {
    agent none
    stages {
        stage('Run Tests') {
            parallel {
                stage('Test On Windows') {
                    agent {
                        label "windows"
                    }
                    steps {
                        echo "test done"
                    }
                }
                stage('Test On Linux') {
                    agent {
                        label "linux"
                    }
                    steps {
                        echo "test done"
                    }
                 }
            }
        }
    }
}

  stage 'package'
  echo "Do package jobs"

  stage 'preview'
  echo 'Do preview jobs'

  try{
    stage 'Approve, go production'
    def url = 'http://localhost:8080/'
    input message: "Does staging at $url look good? ", ok: "Deploy to production"
  }
  finally{
    echo "Remove the resources and send the result mail to DevOps"
  }

  stage 'deploy'
  echo 'Deployment to production'
}
