pipeline{
  agent any
    triggers{
      upstream(upstreamProjects: 'maven sample project' , threshold: hudson.model.Result.SUCCESS)
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

 stage('rt server'){
           steps{
               rtServer (
                   id: 'Jfrog-OSS',
                   url: 'http://51.20.41.73:8082/artifactory',
                   username: 'admin',
                   password: 'Riyansh@08',
                   bypassProxy: true,
                   timeout: 300
               )

           }
       }

stage('rt upload'){
           steps{
               rtUpload (
                   serverId: 'JFROG-OSS',
                   spec: '''{
                         "files": [
                             {
                                 "pattern": "multi-module/server/target/*.jar",
                                 "target": "test2/"

                             }
                                  ]
                   }''',
                        
               )

           }
   }
  }
}
