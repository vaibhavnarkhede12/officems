
we shhud surely use this so that we can find the keys and cred  before code is pushed to github

PR_COMMIT=$(git rev-parse refs/remotes/origin/pull/$CHANGE_ID/head)
echo $PR_COMMIT
