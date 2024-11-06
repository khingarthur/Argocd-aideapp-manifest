node {
    def app
    
    env.IMAGE = 'khingarthur/aide-app'

    stage('Clone repository') {
             git branch: 'main', url: 'https://github.com/khingarthur/Argocd-aideapp-manifest.git'  
    }

    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'Github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        //script {def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')}
                        //script  {def IMAGE='khingarthur/aide-app'}
                        sh "git config user.email arthurfrederick03@gmail.com"
                        sh "git config user.name Khingarthur"
                        sh "cat deployment.yml"
                        sh "sed -i 's+${IMAGE}.*+${IMAGE}:${DOCKERTAG}+g' deployment.yml"
                        sh "cat deployment.yml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job,updated manifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/Argocd-aideapp-manifest.git HEAD:main"
             }
         }
     }
  }
}
