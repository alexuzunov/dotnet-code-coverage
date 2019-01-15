pipeline {
    environment {
      scannerHome = tool 'sonarscanms'
    }
    agent any

    stages {
        stage('Build') {
            steps {
              withSonarQubeEnv('Sonar') {
                // SonarScanner.MSBuild.dll is being called by this python script
                sh 'python3 bin/build.py -k dotnet-local'
              }
            }
        }
        stage('Quality Gate') {
          steps {
            timeout(time: 1, unit: 'HOURS') {
              waitForQualityGate abortPipeline: true
            }
          }
        }
    }
}
