node {
    stage 'Checkout'

    def scmVars = checkout scm
    def commitHash = scmVars.GIT_COMMIT
    println commitHash
    echo sh(returnStdout: true, script: "git log --pretty=%P -n 1 ${commitHash}")
    echo sh(returnStdout: true, script: "git show -s --pretty=%P ${commitHash}")
    echo sh(returnStdout: true, script: "git rev-list --parents -n 1 ${commitHash}")
    
    if (env.CHANGE_ID) {
        println pullRequest.head
    }
    
    echo sh(returnStdout: true, script: "git symbolic-ref refs/remotes/origin/HEAD | sed 's@^refs/remotes/origin/@@'")
    

    stage 'Env'
    echo sh(returnStdout: true, script: 'env')
    
    stage 'SQ'
    withEnv(["PATH+SQ=${tool '3.3'}/bin"]) {
      withSonarQubeEnv {
        sh 'sonar-scanner -Dsonar.projectKey=test-with-jenkins'
      }    
    }
}   
