pipeline {
  agent any
  options { timestamps(); disableConcurrentBuilds() }
  triggers { githubPush() }
  stages {
    stage('Checkout') { steps { checkout scm } }
    stage('Install') { steps { sh 'python3 -m venv .venv && . .venv/bin/activate && pip install -r requirements.txt' } }
    stage('Validate') { steps { sh 'python -m compileall -q app.py' } }
    stage('Deploy') { steps { sh 'sudo rsync -a --delete app.py requirements.txt /opt/tutedude/flask/ && sudo systemctl restart flask.service && sudo systemctl is-active --quiet flask.service' } }
  }
  post { always { cleanWs() } }
}
