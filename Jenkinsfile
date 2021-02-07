// this is a sample jenkinsfile structure (declarative)

pipeline{

  agent any
  
  parameters{
    string(name: 'VERSION', defaultValue: 'abc', description: 'This is the version to deploy on prod')
    booleanParam(name: extecuteTests, defaultValue: true, description: 'run tests if true')
  }
  environment{
    NEW_VERSION='1.2.3'
    SERVER_CREDENTIALS = credentials('')
  }
  
  tools{
    maven 'Maven'
  }
  
  stages{
    stage(" git checkout"){
      steps{
        echo 'pulling code from GIT'
      }
    }
    
    stage(" build app"){
    // will run only if the condition is true
      when{
        expression{
          BRANCH_NAME = 'DEV' || BRANCH_NAME = 'MASTER' && CODE_CHANGES== TRUE
        }
      }
       steps{
        echo "builing the app with version ${NEW_VERSION}"
      }
    }
    
    stage("Testing"){
      when{
        expression{
          params.extecuteTests == true
        }
    steps{
        echo 'testing the app'
      }
    }
    
    stage("Deploying"){
    steps{
        echo 'deploying the app'
      }
    }
  
  }

post{
  always{
    // always runs this 
    // like sending email on build status
  }
  success{
    // only if build passes
  }
  failure{
  // only if build failed
  }
}

}
