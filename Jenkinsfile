node {
   def app

   stage('Clone repository') {

      checkout scm

}

stage('Update GIT') {
        script {
            catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
		withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
		    //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD", 'UTF-B')
		    sh "git config user.email sazib@comptech.com.bd.com"
		    sh "git config user.name rakibhasansazib"
		    //sh "git switch master"
		    sh "cat deployment.yaml"
		    sh "sed -i 's+rakibhasansazib/test .* +rakibhasansazib/test:${DOCKERTAG}+g' deployment.yaml"
		    sh "cat deployment.yaml"
		    sh "git add ."
		    sh "git comnit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
		    sh "git push https://${GIT_USERNAME):${GIT_PASSWORD}@github.com/${GIT_USERNAME}/k8smanifest.git HEAD:main"
		    }
		}
	   }
	}
}
