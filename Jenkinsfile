node {
    def app

    stage('Update GIT') {
        script {
            catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                    // def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                    sh "git config user.email parameswarankrishnan36@gmail.com"
                    sh "git config user.name Parameswaran009"
                    // sh "git switch main"
                    sh "cat deployment.yaml"
                    sh "sed -i 's+username/reponame.*+username/reponame:${DOCKERTAG}+g' deployment.yaml"
                    sh "cat deployment.yaml"
                    sh "git add ."
                    sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                    sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/kubernetesmanifest.git HEAD:main"
                }
            }
        }
    }
}
