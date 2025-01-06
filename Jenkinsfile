pipeline {
    agent any

    stages {
        stage('Test') {
            steps {
                bat './gradlew test'
                archiveArtifacts 'build/test-results/'
                cucumber(
                    reportTitle: 'My report',
                    fileIncludePattern: 'reports/example-report.json',
                    trendsLimit: 10,
                    classifications: [
                        [
                            'key': 'Browser',
                            'value': 'Firefox'
                        ]
                    ]
                )
                junit 'build/test-results/test/TEST-Matrix.xml'
            }
        }
        stage('Code Analysis') {
                    steps {
                         withSonarQubeEnv('sonar') {
                            bat './gradlew sonarqube'
                        }
                    }
        }
//        stage('Code Quality') {
//                    steps {
 //                       waitForQualityGate abortPipeline: true
  //                  }
        stage("Build") {
              steps {
                  bat './gradlew.bat build'
                  bat './gradlew.bat javadoc'
                  archiveArtifacts 'build/libs/*.jar'
                  archiveArtifacts 'build/docs/'

              }
        }

    }
}
