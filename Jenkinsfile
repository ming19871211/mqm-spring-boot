pipeline {
    agent {//项目编译的环境
        docker {
            image 'maven:3-jdk-8'
            label 'docker-server'  //有docker服务的节点
            args '-v /data/maven-repo:/data/maven-repo -v /app/maven/apache-maven-3.5.0/conf/settings.xml:/usr/share/maven/conf/settings.xml'
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