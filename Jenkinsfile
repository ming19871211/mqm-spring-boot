pipeline {
    agent {//项目编译的环境
        docker {
            image 'maven:3-alpine'
            label 'docker-server'  //有docker服务的节点
            args '-v /data/maven-repo:/root/.m2'
        }
    }
    stages{
	    stage('download') {//下载项目
	    	echo 'download ...'
	    	git credentialsId: 'ebbfc189-551d-45b3-97d7-24ac5af6da89', url: 'https://github.com/ming19871211/mqm-spring-boot.git'
	    }
	    stage('Build') {//编译
	    	echo 'build...'
	    	sh 'mvn -B -DskipTests clean package'
	        //sh 'mvn clean package -Dmaven.test.skip=true'
	    }    
	    stage('Test') {//测试
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