pipeline {
  agent {
    docker {
      // Testing pipeline V1.0
      image 'returntocorp/semgrep-agent:v1'
      args '-u root'
    }
  }
  
  enviroment {
    // Semgrep org ID and authentication token, another comment
    SEMGREP_APP_TOKEN = credentials('SEMGREP_APP_TOKEN')
    SEMGREP_DEVELOPMENT_ID = credentials('SEMGREP_DEVELOPMENT_ID')
    
    //envrioment variables for semgrep-agent
    // remove .git at the end
    SEMGREP_REPO_URL = env.GIT_URL.replaceFirst(/^(.*).git$/,'$1')
    SEMGREP_BRANCH = "${GIT_BRANCH}"
    SEMGREP_JOB_URL = "${BUILD_URL}"
    // remove SCM URL + .git at the end
    SEMGREP_REPO_NAME = env.GIT_URL.replaceFirst(/^https:\/\/github.com\/(.*).git$/, '$1')
  }
  
  stages {
    stage('Semgrep_agent') {
      steps{
        sh 'python -m semgrep_agent --publish-token $SEMGREP_APP_TOKEN --publish-development $SEMGREP_DEPLOYMENT_ID'
      }
    }
  }
}
