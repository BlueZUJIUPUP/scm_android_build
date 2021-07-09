pipeline{
    agent any
    options {
        ansiColor('xterm')
    }
    stages{
        //这里将Jenkinsfile和要编译的代码分开存放
        //默认拉取Jenkinsfile  然后按照里面的pipeline来设置拉取代码和后续操作
        stage("代码下载"){
            steps {
				checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [[$class: 'RelativeTargetDirectory', relativeTargetDir: 'test_android']], userRemoteConfigs: [[url: 'https://gitee.com/blue-juziupup/test_android.git']]])
            }
        }
        //build
        stage("build"){
            steps {	
				gradlew clean assembleDebug	
            }
        }
		//sonar检查
		stage("sonar检查"){
            steps {
				gradlew sonarqube \
  -Dsonar.projectKey=scm_jenkins_file \
  -Dsonar.host.url=http://192.168.171.128:9000 \
  -Dsonar.login=8dfbed8f376f2bc4a101c33aec0d53bf43cbc053							
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