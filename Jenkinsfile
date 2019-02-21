node ('beaware-jenkins-slave') {
    stage('Download Latest') {
	if (env.BRANCH_NAME != 'master') {
		autoCancelled = true
		return
	}
        git(url: 'https://github.com/beaware-project/text-analysis-all.git', branch: 'master')
        sh 'git submodule init'
        sh 'git submodule update'
    }

    stage ('Deploy') {

        sh 'kubectl apply -f kubernetes/deploy.yaml -n prod --validate=false'
    }

    stage ('Print-deploy logs') {
        sh 'sleep 60'
        sh 'kubectl  -n prod logs deploy/concept-candidates'
    }
}
