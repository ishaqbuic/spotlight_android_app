def commitContainsSkip = 0

pipeline {
  agent {
        label 'tester_node'
      }

  
  //options {
    // Stop the build early in case of compile or test failures
   // skipStagesAfterUnstable()
 // }

  stages {

    stage('Init') {
            steps {
                script {
                    
                    commitContainsSkip = sh(script: "git log -1 | grep '.*\\[start build\\].*'", returnStatus: true)
              }
                sh "echo $commitContainsSkip"
            }
        }


    stage('Git commit Status'){
      steps{
        sh "git log -1 > lastCommitMsg.txt"
        sh "cat lastCommitMsg.txt"
        sh "ls"
        //scmSkip(deleteBuild: true, skipPattern:'.*\\[ci skip\\].*')
      }
    }   
    stage('Build and Deploy') {
       when {
          expression { commitContainsSkip == 0 }
     }
      agent {
        docker {
          args '-u root:root'
          image 'mtayyabq/androidci:1.0.0'
          reuseNode true
        }
      }

          
      steps {
        
        //scmSkip(deleteBuild: true, skipPattern:'.*\\[ci skip\\].*')
        //sh 'apt-get update && sudo apt-get upgrade'
        sh 'apt-get -y update'
        sh 'apt-get -y install default-jdk'
        sh 'export GRADLE_USER_HOME=`pwd`/.gradle'
        sh 'chmod +x ./gradlew'
      
        // Compile the app and its dependencies
        sh './gradlew compileDebugSources'

        // Finish building and packaging the APK
        sh './gradlew clean assembleDebug'

        // Archive the APKs so that they can be downloaded from Jenkins
        archiveArtifacts '**/*.apk'


      }
      
    }
    stage('Clean Workspace') {
            steps {
                cleanWs()
            }
        }
        

  }
  
}

