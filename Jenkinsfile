node {
    stage 'Checkout'

    checkout scm

    stage 'Env'
    echo sh(returnStdout: true, script: 'env')
    
    stage 'SQ'
    withEnv(["PATH+SQ=${tool '3.3'}/bin"]) {
      withSonarQubeEnv {
        sh 'sonar-scanner -Dsonar.projectKey=test-with-jenkins'
      }    
    }
}   
