node {

  stage 'checkout project'
  git url: 'https://github.com/wuthomas/jenkinstest.git'

  stage 'check env'

  echo "Set env vars"
  echo "Env vars"

  stage 'test'
  echo "Do the test jobs"

  stage 'package'
  echo "Do package jobs"

  stage 'preview'
  echo 'Do preview jobs'

  try{
    stage 'Approve, go production'
    def url = 'http://localhost:8888/'
    input message: "Does staging at $url look good? ", ok: "Deploy to production"
  }finally{
    echo "ssh jenkins@localhost 'kill `cat deploy/release/run.pid`'"
  }

  stage 'deploy'
  echo 'Deployment to production'
}