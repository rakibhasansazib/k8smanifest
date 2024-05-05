node {
    def app

    stage('Clone repository') {
        checkout scm
    }

    stage('Update GIT') {
        script {
            catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                    sh "git config user.email sazib@comptech.com.bd"
                    sh "git config user.name rakibhasansazib"
                    sh "cat deployment.yaml"
                    sh "sed -i 's+rakibhasansazib/test.*+rakibhasansazib/test:${DOCKERTAG}+g' deployment.yaml"
                    sh "cat deployment.yaml"
                    sh "git add ."
                    sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                    sh "git push @github.com/${GIT_USERNAME}/k8smanifest.git">https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/k8smanifest.git HEAD:main"
                }
            }
        }
    }
}
