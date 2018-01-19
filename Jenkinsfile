node {

  stage 'checkout project'
  checkout scm

  stage 'check env'

  echo "Set env vars"
  echo "Print env vars"
  sh 'printenv'

  stage 'Test' {
    parallel linux: {
            node('linux') {
	        echo "checkout T1 project"
	        checkout scm
	        sleep 5
	        echo "Test T1 job done"
        },
            windows: {
            node('windows') {
	        echo "Checkout T2 project"
	        checkout scm
	        sleep 15
	        echo "Test T2 job done"
        },
	    other: {
            node('other') {
	        echo "checkout T3 project"
	        checkout scm
	        sleep 10
	        echo "Test T3 job done"
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
