pipeline {
  agent any
  stages {
    stage('Preparation Step') {
      steps {
        bat 'git bisect start'
        bat 'git bisect bad 198644632661c67b6c32f59e9047c11a70685e15'
        bat 'git bisect good 98ac319c0cff47b4d39a1a7b61b4e195cfa231e5'
      }
    }

    stage('Git Bisect Step') {
      steps {
        script {
          def runMavenTest = {
            try {
              bat 'mvn clean test'
              return true
            } catch (any) {
              return false
            }
          }
          bat 'git bisect run powershell -Command "if(runMavenTest) { exit 0 } else { exit 1 }"'
        }

      }
    }

    stage('Final step completed') {
      steps {
        bat 'git bisect reset'
      }
    }

  }
  tools {
    maven 'JOHN_MVN'
    jdk 'JOHN_JDK'
  }
}