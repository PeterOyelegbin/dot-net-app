def gv

pipeline {
  agent any
  //tools {
    //maven "maven-3.9"
  //}
  environment {
    NEW_VERSION = "1.0.3"
    //GITHUB_CREDENTIALS = credentials('github-cred')
  }
  parameters {
    //string(name: 'VERSION', defaultValue: '', description: 'version to deploy on Prod')
    choice(name: 'VERSION', choices: ['1.1.0', '1.2.0', '1.3.0'], description: '')
    booleanParam(name: 'PRODUCTION', defaultValue: false, description: '')
  }
  stages {
    stage("init") {
      steps {
        script {
          gv = load "script.groovy"
        }
      }
    }
    stage("test") {
      when {
        expression {
          env.BRANCH_NAME == 'dev' || env.BRANCH_NAME == 'main'
        }
      }
      steps {
        echo "test stage with version ${NEW_VERSION}."
      }
    }
    stage("build") {
      when {
        expression {
          env.BRANCH_NAME == 'main'
        }
      }
      steps {
        script {
          gv.buildApp
        }
      }
    }
    stage("deploy") {
      when {
        expression {
          params.PRODUCTION == true
        }
      }
      input {
        message "Select the environment to deploy to"
        ok "Done"
        parameters {
          choice(name: 'ENV', choices: ['dev', 'staging', 'prod'], description: '')
        }
      }
      steps {
        script {
          gv.deployApp
          echo "Deploying to ${ENV}"
        }
      }
    }
  }
  //post {
    //always {
      //
    //}
    //success {
      // 
    //}
    //failure {
      //
    //}
  //}
}
