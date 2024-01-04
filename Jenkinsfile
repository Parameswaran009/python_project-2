pipeline {
    agent any

    stages {
        stage('Initialization') {
            steps {
                script {
                    // Clone the Git repository
                    checkout scm
                }
            }
        }

        stage('Update GIT') {
            steps {
                script {
                    catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                        withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                            sh "git config user.email parameswarankrishnan36@gmail.com"
                            sh "git config user.name Parameswaran009"
                            sh "cat deployment.yaml"
                            sh "sed -i 's+username/reponame.*+username/reponame:${DOCKERTAG}+g' deployment.yaml"
                            sh "cat deployment.yaml"
                            sh "git add ."
                            sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                            sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/python_project-2.git HEAD:main"
                        }
                    }
                }
            }
        }
    }
}
