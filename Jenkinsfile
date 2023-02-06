node{
   stage('Git'){
     git 'https://github.com/refnijam/my-app.git'
   }
   stage('Build Maven Compile-Package')
   {

     def mvnHome =  tool name: 'maven3', type: 'maven'   
      sh "${mvnHome}/bin/mvn clean package"
	  sh 'mv target/myweb*.war target/newapp.war'
   }
 stage('Build Docker Imager'){
   sh 'docker build -t nijamnar/demo:0.0.1 .'
   }
   stage('Docker Image Push'){
   withCredentials([string(credentialsId: 'dockerPass', variable: 'dockerPassword')]) {
   sh "docker login -u nijamnar -p ${dockerPassword}"
    }
   sh 'docker push nijamnar/demo:0.0.1'
   }
}
