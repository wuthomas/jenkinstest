node {

  stage 'checkout project'
  git url: 'https://github.com/wuthomas/jenkinstest.git'

  stage 'check env'

  echo "Set env vars"
  echo "Env vars"

  stage 'parallel-testing' {
    parallel {
	stage ('check one') {
	    echo "Do check job 1"
	    sleep 5
	    echo "Finish check job 1"
        }
	stage ('check two') {
	    echo "Do check job 2"
	    sleep 10
	    echo "Finish check job 2"
        }
	stage ('check three') {
	    echo "Do check job 3"
            sleep 15
            echo "Finish check job 3"
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
