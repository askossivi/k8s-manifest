node {
    def app

    stage('Clone repository') {
      
        checkout scm
    }

    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        sh "git config --global user.email ediguy.com"
                        sh "git config --global user.name Edu Guy"
                        //sh "git switch master"  
                        sh "cat k8s/client-deployment.yml"
                        sh "cat k8s/postgres-deployment.yml"
                        sh "cat k8s/server-deployment.yml"
                        sh "sed -i 's+devtraining/server-app.*+devtraining/server-app:${DOCKERTAG}+g' k8s/server-deployment.yml"
                        sh "sed -i 's+devtraining/client-app.*+devtraining/client-app:${DOCKERTAG}+g' k8s/client-deployment.yml"
                        sh "cat k8s/client-deployment.yml"
                        sh "cat k8s/postgres-deployment.yml"
                        sh "cat k8s/server-deployment.yml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push -f https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/k8s-manifest.git HEAD:main"
      }
    }
  }
}
}
