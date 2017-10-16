node {
   def mvnHome
   stage('Preparation') { // for display purposes
      // Get some code from a GitHub repository
      git 'https://github.com/dlabordus/TDDTrainingApplication.git'
      // Get the Maven tool.
      // ** NOTE: This 'M3' Maven tool must be configured
      // **       in the global configuration.           
      mvnHome = tool 'Maven'
     
      env.JAVA_HOME="${tool 'JDK8'}"
      env.PATH="${env.JAVA_HOME}/bin:${env.PATH}"
      sh 'java -version'
   }
   stage('Build') {
     // Move into directory
      dir('TDDTrainingApplicationCC') {
      // Run the maven build
        if (isUnix()) {
           sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean install"
        } else {
           bat(/"${mvnHome}\bin\mvn" -Dmaven.test.failure.ignore clean install/)
        }
      }
   }
   stage('Results') {
      junit '**/target/surefire-reports/TEST-*.xml'
      archive 'target/*.jar'
   }
}
