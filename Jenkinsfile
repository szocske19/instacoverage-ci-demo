// Tell Jenkins how to build projects from this repository
pipeline {
	agent {
		label 'windows'
	}
	
	parameters {
		string(name: "LV2018_PATH", defaultValue: "C:\\Program Files (x86)\\National Instruments\\LabVIEW 2018\\LabVIEW.exe", description: "")
	}
	
	stages { 
		stage('Build') {				
			steps { 
				timeout(time: 5, unit: 'MINUTES') {	
					bat 'LabVIEWCLI -LabVIEWPath "%LV2018_PATH%" -LogToConsole true -OperationName RunVI -VIPath "%WORKSPACE%\\ci-script.vi" "%WORKSPACE%\\instacoverage-ci-demo.lvproj" "%WORKSPACE%"'
				}
			}
		}
	}		
	post {
        always {
			junit '**/report.xml'
        }
        failure {
			echo 'Pipeline post action Failure.' 
		}
    }
}