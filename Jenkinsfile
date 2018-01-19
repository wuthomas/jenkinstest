node {
  for (int i=0; i< 3; ++i) {  
    stage "Stage #"+i
    print 'Hello, world $i!'
  }

  stage('Checkout'){

      checkout scm
  }

  stage 'check env'

  echo "Set env vars"
  echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}"

  stage 'run-parallel-branches-test1'
      steps{
		  parallel
		  a: {
			  echo "Do test1 for branche master"
			  sleep 5
			  echo "master test1 done"
		  },
		  b: {
			  echo "Do test1 for branche b"
			  sleep 10
			  echo "branch b test1 done"
		  },
		  c: {
			  echo "Do test1 for branche c"
			  sleep 15
			  echo "branch c test1 done"
		  }
  }

  stage 'package'
  echo "Do package jobs"

  stage 'preview'
  echo 'Do preview jobs'

  try{
    stage 'Approve, go production'
    def url = 'http://localhost:8888/'
    input message: "Does staging at $url look good? ", ok: "Deploy to production"
  }finally{
    echo "Remove the resources and send the result mail to DevOps"
  }

  stage 'deploy'
  echo 'Deployment to production'
}