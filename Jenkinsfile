@Library('my-shared-library') _

pipeline{

    agent any


    environment {
    CI = true
    ARTIFACTORY_ACCESS_TOKEN = credentials('artifactory-access-token')
  }
    //agent { label 'Demo' }

    parameters{

       choice(name: 'action', choices: 'create\ndelete', description: 'Choose create/Destroy')
        string(name: 'ImageName', description: "name of the docker build", defaultValue: 'javapp')
       string(name: 'ImageTag', description: "tag of the docker build", defaultValue: 'v1')
       string(name: 'DockerHubUser', description: "name of the Application", defaultValue: 'mrunali095')
     }

    stages{
         
        stage('Git Checkout'){
                    when { expression {  params.action == 'create' } }
            steps{
            gitCheckout(
                branch: "main",
                url: "https://github.com/mrunali154/Java_app_3.0.git"
            )
            }
        }
         stage('Unit Test maven'){
         
         when { expression {  params.action == 'create' } }

            steps{
               script{
                   
                   mvnTest()
               }
            }
        }
         stage('Integration Test maven'){
         when { expression {  params.action == 'create' } }
            steps{
               script{
                   
                   mvnIntegrationTest()
               }
            }
        }
        // new code

    stage('Push to JFrog') {
      
      steps {
        sh 'jfrog rt upload --url http://192.168.1.230:8082/artifactory/ --access-token ${ARTIFACTORY_ACCESS_TOKEN} target/kubernetes-configmap-reload-0.0.1-SNAPSHOT.jar Java_app_3.0/'
      }
    }

//sample
//         stage('Push to JFrog'){
// when { expression {  params.action == 'create' } }
//             steps{
//                script{
//                 //Connect artifactory
//                 def server = Artifactory.server 'Pushartifact'
//                 // upload file
//                 def uploadSpec = """{
//                         "files": [
//                             {
//                                 "pattern": "target/*.jar",
//                                 "target": "example-repo-local/"
//                             }
//                        ]
//                 }"""
//                 //upload artifact to jfrog
//                 server.upload(uploadSpec)
//         }
//   }
// }
        //sample
 
       //  stage('Static code analysis: Sonarqube'){
       //   when { expression {  params.action == 'create' } }
       //      steps{
       //         script{
                   
       //             def SonarQubecredentialsId = 'sonarqube-api'
       //             statiCodeAnalysis(SonarQubecredentialsId)
       //         }
       //      }
       // }
       // stage('Quality Gate Status Check : Sonarqube'){
       //   when { expression {  params.action == 'create' } }
       //      steps{
       //         script{
                   
       //             def SonarQubecredentialsId = 'sonarqube-api'
       //             QualityGateStatus(SonarQubecredentialsId)
       //         }
       //      }
       // }
       //  stage('Maven Build : maven'){
       //   when { expression {  params.action == 'create' } }
       //      steps{
       //         script{
                   
       //             mvnBuild()
       //         }
       //      }
       //  }
       //  stage('Docker Image Build'){
       //   when { expression {  params.action == 'create' } }
       //      steps{
       //         script{
                   
       //             dockerBuild("${params.ImageName}","${params.ImageTag}","${params.DockerHubUser}")
       //         }
       //      }
       //  }
       //   stage('Docker Image Scan: trivy '){
       //   when { expression {  params.action == 'create' } }
       //      steps{
       //         script{
                   
       //             dockerImageScan("${params.ImageName}","${params.ImageTag}","${params.DockerHubUser}")
       //         }
       //      }
       //  }
       //  stage('Docker Image Push : DockerHub '){
       //   when { expression {  params.action == 'create' } }
       //      steps{
       //         script{
                   
       //             dockerImagePush("${params.ImageName}","${params.ImageTag}","${params.DockerHubUser}")
       //         }
       //      }
       //  }   
       //  stage('Docker Image Cleanup : DockerHub '){
       //   when { expression {  params.action == 'create' } }
       //      steps{
       //         script{
                   
       //             dockerImageCleanup("${params.ImageName}","${params.ImageTag}","${params.DockerHubUser}")
       //         }
       //      }
       //  }      
    }
}
