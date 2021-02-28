  
node{
   stage('SCM Checkout'){
     git 'https://github.com/gopigl/sample'
   }
   stage('Compile-Package'){
      // Get maven home path
      def mvnHome =  tool name: 'maven-3', type: 'maven'   
      sh "${mvnHome}/bin/mvn clean package"
   }
   
   stage('SonarQube Analysis') {
        def mvnHome =  tool name: 'maven-3', type: 'maven'
        withSonarQubeEnv('Sonar') { 
          sh "${mvnHome}/bin/mvn sonar:sonar"
        }
    }
  
   stage('Deploy to Tomcat'){
      
      sshagent(['tomcat-dev']) {
         sh 'scp -o StrictHostKeyChecking=no target/*.jar ec2-user@54.90.115.129:/opt/tomcat9/webapps/'
      }
   }
   
   

}
