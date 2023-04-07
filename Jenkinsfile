node {
    def app
            
      stage('Clone repository') {
        checkout scm
        echo "git cloned"
      }

      stage('Update GIT') {
        script {
            catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
               withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                  //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                  echo "update git starts"
                  sh "git config --global user.email sandeep.cris@gmail.com"
                  sh "git config --global user.name sandeepcris"
                  //sh "git switch master"
                  sh "cat deployment.yaml"
                  sh "sed -i 's+sandeepcris/myweb:.*+sandeepcris/myweb:${DOCKERTAG}+g' deployment.yaml"
                  sh "cat deployment.yaml"
                  sh "git add ."
                  sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                  sh "git config -l"
                  sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/jenkins-demo-manifest.git HEAD:main"
               }
            } 
        }
      }
}
