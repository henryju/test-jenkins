node {
    stage 'Checkout'

    def scmVars = checkout scm
    def commitHash = scmVars.GIT_COMMIT
    println commitHash

    stage 'Env'
    echo sh(returnStdout: true, script: 'env')
    
    stage 'SQ'
    withEnv(["PATH+SQ=${tool '3.3'}/bin"]) {
      withSonarQubeEnv {
        sh 'sonar-scanner -Dsonar.projectKey=test-with-jenkins'
      }    
    }
}   
