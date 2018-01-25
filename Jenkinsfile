pipeline {
    agent {//项目编译的环境
        docker {
            image 'maven:3.5.2-jdk-8-alpine'
            label 'docker-server'  //有docker服务的节点
            args '-v /data/maven-repo:/root/.m2/repository'
        }
    }
    stages{
	    stage('Build') { //编译
	    	steps{
		    	echo 'build...'
		    	sh 'mvn -B -DskipTests clean package'
		        //sh 'mvn clean package -Dmaven.test.skip=true'
		    }
	    }    
	    stage('Test') { //测试
		    steps {
		        sh 'mvn test' 
		    }
		    post {
		        always {
		            junit 'target/surefire-reports/*.xml' 
		        }
		    }
		}
    }   
}