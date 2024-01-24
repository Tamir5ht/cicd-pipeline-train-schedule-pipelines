pipeline {

    agent {
        node {
            label 'master'
        }
    }

    options {
        buildDiscarder logRotator( 
                    daysToKeepStr: '16', 
                    numToKeepStr: '10'
            )
    }

    stages {
        
        stage('Cleanup Workspace') {
            steps {
                cleanWs()
                sh """
                echo "Cleaned Up Workspace For Project"
                """
            }
        }

        stage('Build Deploy Code') {
            when {
                branch 'master'
            }
            steps {
                sh """
                echo "Building Artifact"
		sleep 180
		./gradlew build --no-daemon
                """
		 archiveArtifacts artifacts: 'dist/trainSchedule.zip', fingerprint: true

                sh """
                echo "Deploying Code"
                """
            }
        }

    }   
}
