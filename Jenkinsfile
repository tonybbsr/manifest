node {
    def app

    stage('Clone repository') {
      

        checkout scm
    }

    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                     withCredentials([string(credentialsId: 'github-token', variable: 'GITHUB_TOKEN')]) {
                        //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        sh 'export GIT_USERNAME=tonybbsr'
                        sh "git config user.email tonybbsr@gmail.com"
                        sh "git config user.name tonybbsr"
                        //sh "git switch main"
                        sh "cat deployment.yml"
                        sh "sed -i 's+tonybbsr/demo.*+tonybbsr/demo:${DOCKERTAG}+g' deployment.yml"
                        sh "cat deployment.yml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GITHUB_TOKEN}@github.com/tonybbsr/manifest.git HEAD:main"
      }
    }
  }
}
}
