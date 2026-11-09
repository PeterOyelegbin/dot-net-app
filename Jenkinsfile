CODE_CHANGES = getGitChanges()
pipeline {
  agent any
  environment {
    NEW_VERSION = '1.0.3'
    //SERVER_CREDENTIALS = credentials('')
  }
  parameters {
    //string(name: 'VERSION', defaultValue: '', description: 'version to deploy on Prod')
    choice(name: 'VERSION', choices: ['1.1.0', '1.2.0', '1.3.0'], description: '')
    booleanParam(name: 'PRODUCTION', defaultValue: false, description: '')
  }
  stages {
    stage("test") {
      when {
        expression {
          BRANCH_NAME == 'dev' || BRANCH_NAME == 'main'
        }
      }
      steps {
        echo "test stage with version ${NEW_VERSION}."
      }
    }
    stage("build") {
      when {
        expression {
          BRANCH_NAME == 'dev' && CODE_CHANGES == true
        }
      }
      steps {
        echo "build stage"
      }
    }
    stage("deploy") {
      when {
        expression {
          params.PRODUCTION == True
        }
      }
      steps {
        echo "deploy stage"
      }
    }
  }
  post {
    always {
      //
    }
    success {
      // 
    }
    failure {
      //
    }
  }
}
