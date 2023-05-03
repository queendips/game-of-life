node('game-of-life') {
	stage ('git checkout') {
		git branch: 'dev1', url: 'https://github.com/queendips/game-of-life.git'

}
 	stage('Build the code') {
       		sh 'mvn clean package'
}
	stage('archiving the code') {
		junit '**/surefire-reports/*.xml'
		archiveArtifacts artifacts: '**/*.war', followSymlinks: false
}  

}

