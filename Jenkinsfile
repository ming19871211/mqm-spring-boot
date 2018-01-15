node {
    echo 'this is "Hello World"'
    //git credentialsId: 'ebbfc189-551d-45b3-97d7-24ac5af6da89', url: 'https://github.com/ming19871211/mqm-spring-boot.git'
    //def mvnHome = tool 'apache-maven-3.5.0' 
    //sh "${mvnHome}/bin/mvn -B verify"
    def serverPath = '/app/springboot/jenkins-jar'
    stage('download') {
    	echo '下载源码'
    	git credentialsId: 'ebbfc189-551d-45b3-97d7-24ac5af6da89', url: 'https://github.com/ming19871211/mqm-spring-boot.git'
    }
    stage('Test') {
        echo '测试源码包'
        sh "mvn -B verify"
    }
    stage('Build') {
    	echo  'maven打包'
        sh 'mvn clean package -Dmaven.test.skip=true'
    }    
    stage('upload') {
    	echo 'upload'
    	sh 'mv ${env.WORKSPACE}/target/*.jar ${serverPath}'
    }
    stage('Deploy') {
        sh 'cd ${serverPath}'
        sh 'java -jar *.jar > log.file 2>&1 &'
    }
    
    post {
        always {
            junit '**/target/*.xml'
        }
        failure {
        	echo '编译失败'
            //mail to: ming19871211@163.com, subject: 'The Pipeline failed :('
        }
    }
}