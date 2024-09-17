
we shhud surely use this so that we can find the keys and cred  before code is pushed to github

PR_COMMIT=$(git rev-parse refs/remotes/origin/pull/$CHANGE_ID/head)
echo $PR_COMMIT


pipeline {
    agent any

    stages {
        stage('Check Changed Files for ../../modules') {
            steps {
                script {
                    // Get the list of changed files in the latest commit
                    def changedFiles = sh(script: "git diff --name-only HEAD~1 HEAD", returnStdout: true).trim()

                    // Check if any of the changed files contains '../../modules'
                    def matchFound = false

                    changedFiles.split('\n').each { file ->
                        def fileContent = sh(script: "git show HEAD:${file}", returnStdout: true)
                        if (fileContent.contains('../../modules')) {
                            matchFound = true
                            echo "Match found in file: ${file}"
                        }
                    }

                    if (matchFound) {
                        echo "Pattern '../../modules' found in changed files!"
                    } else {
                        echo "No match for pattern '../../modules' in the changed files."
                    }
                }
            }
        }
    }
}
