env.WORKSPACE = "D:/test_jenkins/test"

pipeline{
    agent any
	
    stages { 
	
		stage('start') { 
			steps {   
				echo 'Hello World'
				}
			}
			
        stage("download-code"){
            steps {
				dir(env.WORKSPACE){
					checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [[$class: 'RelativeTargetDirectory', relativeTargetDir: 'test_android']], userRemoteConfigs: [[url: 'https://gitee.com/blue-juziupup/test_android.git']]])
					}
				}	
			}
		stage("build"){
            steps {	
				dir(env.WORKSPACE/test_android){
					bat 'gradlew clean assembleDebug'	
				}
			}
		}
	}
}