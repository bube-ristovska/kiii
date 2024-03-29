node {
    def app
  if (env.BRANCH_NAME == 'dev') {
    stage('Clone repository') {
        checkout scm
    }

    stage('Build image') {
        app = docker.build("buberistovska/kiii")
    }

    stage('Push image') {   
      
            docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
                app.push("${env.BRANCH_NAME}-latest")
                // signal the orchestrator that there is a new version
            }
        }
     } else {
            echo "Skipping image push as not on 'dev' branch"
    }
    
}
