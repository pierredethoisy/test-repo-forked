pipeline{
triggers {
  pollSCM 'H/2 * * * *'
}
    agent {
        kubernetes{
            defaultContainer 'agent'
            yaml '''apiVersion: v1
kind: Pod
metadata:
  labels:
    app: agent
spec:
  containers:
    - name: agent
      image: jenkins/inbound-agent
      command:
      - cat
      tty: true'''
        }
    }
    environment {
        GITGUARDIAN_API_KEY = '[removed key]'
    }
    stages{
      stage('scan'){
          steps{
              sh 'env | sort'
              // sh 'git config --global --add safe.directory "*"'
              // sh 'git config --global --add safe.repository "https://github-dev.travp.net/gts/delegationkeytest.git"'
              // sh 'ggshield secret scan ci'
          }
      }
    }
}
