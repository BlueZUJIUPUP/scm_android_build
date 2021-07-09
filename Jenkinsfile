env.WORKSPACE = "D:/test_jenkins/test"
env.sonarqube_servers="http://192.168.171.128:9000/"

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
				dir(env.WORKSPACE+"/test_android"){
					bat 'gradlew clean assembleDebug'	
				}
			}
		}
		stage("sonar"){
            steps {
				dir(env.WORKSPACE+"/test_android"){
					withSonarQubeEnv('sonarqube') {
						bat "gradlew sonarqube -Dsonar.projectKey='scm_jenkins_file' -Dsonar.host.url={env.sonarqube_servers} -Dsonar.login=83a42d8762d945d38427a4ddf9bb9dc8522acf2c"							
					}
				}
			}
        }
		
		stage("test"){
            steps {	
				echo "test"	
				}
		}
	}
}