pipeline {
    agent any
    environment {
        IMAGE_FAMILY = 'your-image-family'
        IMAGE_PROJECT = 'your-image-project'
    }
    stages {
        stage('Check GCP Image') {
            steps {
                script {
                    def result = sh(
                        script: """
                            gcloud compute images list --filter="family:${IMAGE_FAMILY}" --project=${IMAGE_PROJECT} --format="get(name)" --limit=1
                        """,
                        returnStdout: true
                    ).trim()
                    if (result) {
                        echo "An image exists in the family ${IMAGE_FAMILY}."
                    } else {
                        error "No image found in the family ${IMAGE_FAMILY}."
                    }
                }
            }
        }
    }
}
