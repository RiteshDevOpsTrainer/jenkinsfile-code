node {
   stage('get-code') {
     git branch: 'main', changelog: false, credentialsId: 'Github-repo-access', url: 'git@github.com:RiteshDevOpsTrainer/devops-june-21.git'
   }
   stage('build') {
     def mvnHome = tool 'MVN_HOME'
	 withEnv(["MVN=$mvnHome"]){
	  sh '$MVN/bin/mvn clean compile package'
	 }
   }
   stage('deploy') {
     deploy adapters: [tomcat9(credentialsId: '315a423f-0c50-43c3-91f2-a392fb7fa13f', path: '', url: 'http://172.31.7.57:8080/')], contextPath: null, war: '**/*war'
   }
   stage('notification') {
     emailext body: '''Hello Team,

	$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS:

	Check console output at $BUILD_URL to view the results.''', subject: 'From Pipeline : $PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS!', to: 'ankushharde15@gmail.com, ravikantbnc@gmail.com, jitendradeore92@gmail.com, cc:ritesh.goyal590@gmail.com'
   }
}
