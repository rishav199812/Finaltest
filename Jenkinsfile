def gettarget(branch) {
        if (branch == "origin/master") {
                return 'prod'
        } else {
                return 'dev'
        }

}
pipeline {
  agent any
 environment {
  		region = 'eu-west-1'
		ENV = gettarget(env.GIT_BRANCH)
	} 
    stages {
        stage('Printing Parameters') {
            steps {
                echo "${env.ENV}"
            }
        }

        stage("create lambda zip based on tag") {
            steps {
              echo "Environment to be deployed : ${ENV}" 
             echo "${env.GIT_BRANCH}"
              sh 'printenv'
              echo "${CURRENT_BRANCH_NAME}"
              
              script {
                     DIR_SIZE = sh(returnStdout: true, script: "git describe --tags `git rev-list --tags --max-count=1` ")
                }
                echo "${DIR_SIZE}"
               script {
                   BIR_SIZE = sh(returnStdout: true, script: "git branch -a --contains ${DIR_SIZE}")
               }
               echo "${BIR_SIZE}"
              script {
                 GIR_SIZE = sh(returnStdout: true, script: "git branch -a --contains tags/${DIR_SIZE}")
                echo "${GIR_SIZE}"
              } 
              
              
               
            }
        }
   
                
   
            }
}
