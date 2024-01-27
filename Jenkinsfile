pipeline {

    agent any

    triggers {
        githubPush()
    }

    options {
        buildDiscarder logRotator( 
                    daysToKeepStr: '16', 
                    numToKeepStr: '10'
            )
    }

    stages {
        
        stage('Build Deploy Code') {
            when {
                branch 'master'
            }
            steps {
                sh """
                echo "Building Artifact"
		sleep 3600
		./gradlew build --no-daemon
		echo "done!!!"
                """
		 archiveArtifacts artifacts: 'dist/trainSchedule.zip', fingerprint: true

                sh """
                echo "Deploying Code"
                """
            }
        }

    }   
}
