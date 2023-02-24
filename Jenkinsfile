node('JDK8') {
	stage('source code') {
		git branch: 'sprint1_develop', url: 'https://github.com/queendips/game-of-life.git'
         }
	stage('Build the code') {
			sh 'mvn clean package'
	}
	stage('Archiving and Test result') {
				junit '**/surefire-reports/*.xml'
				archiveArtifacts artifacts: '**/*.war', followSymlinks: false
       }
				
}
