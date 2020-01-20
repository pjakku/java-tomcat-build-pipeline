node{
      def mvnHome = tool name: 'maven', type: 'maven' 
      stage('Checkout'){
         git 'https://github.com/LovesCloud/java-tomcat-build-pipeline'
       
      }  
      stage('Build'){
         //// Get maven home path and build
        sh "${mvnHome}/bin/mvn clean package -Dmaven.test.skip=true"
      }
     stage ('Test-JUnit'){
         sh "'${mvnHome}/bin/mvn' test surefire-report:report"
      }  
    
      stage('Deploy') {     
          sshagent(['tomcatsshuser']) {
               sh 'scp -o StrictHostKeyChecking=no target/demojavapipeline_newuser.war jenkins@35.193.54.220:/opt/tomcat/webapps'
              
          }
         
     }
      
 }
