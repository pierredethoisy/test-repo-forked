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
      image: irgeek/ggshield:v1.14.4
      command:
      - cat
      tty: true'''
        }
    }
    environment {
        GITGUARDIAN_API_KEY = credentials('gitguardian-api-key')
    }
    stages{
      stage('jf'){
          steps{
              sh 'cat Jenkinsfile'
          }
      }
      stage('scan'){
          steps{
              sh 'env | sort'
              sh 'git config --global --add safe.directory "*"'
              sh 'ggshield secret scan ci'
          }
      }
    }
}
