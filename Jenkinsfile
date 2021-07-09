pipeline{
    agent any
    options {
        ansiColor('xterm')
    }
    stages{

        stage("download"){
            steps {
				checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [[$class: 'RelativeTargetDirectory', relativeTargetDir: 'test_android']], userRemoteConfigs: [[url: 'https://gitee.com/blue-juziupup/test_android.git']]])
            }
        }
        //build
        stage("build"){
            steps {	
				sh 'gradlew clean assembleDebug'	
            }
        }

		stage("sonar"){
            steps {
				sh "gradlew sonarqube -Dsonar.projectKey='scm_jenkins_file' -Dsonar.host.url={sonarqube_servers} -Dsonar.login={test01}"							
            }
        }
		//test
        stage("build"){
            steps {	
				echo "test"	
            }
        }
    }
}