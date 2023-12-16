pipeline{
  agent any
    triggers{
      pollSCM('* * * * *')
    }
     stages{
       stage('git clone'){
        steps{ 
           git 'https://github.com/Smooshsri/maven-samples.git'
        }
    }
  stage ('build the code'){
         steps{
            sh 'mvn package'
      }
    }
   stage('archive the artifacts'){
    steps{
      archive 'multi-module/server/target/*.jar'   
}
}
stage('publish junit results'){
   steps{
    junit 'single-module/target/surefire-reports/*.xml'
     
    }
   }
  }
}
