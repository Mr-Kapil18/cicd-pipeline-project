pipeline {
  agent any

  tools {
    maven 'Maven'
  }

  stages {
    stage('Initialize') {
      steps {
        sh '''
          echo "PATH=$PATH"
          echo "M2_HOME=$M2_HOME"
          mvn -version
        '''
      }
    }

   // stage ('Check-Git-Secrets') {
   //   steps {
   //     sh ' trufflehog3 -f json https://github.com/Mr-Kapil18/cicd-pipeline-project.git -o trufflehog_output.json || true '
    //  }
   // }

    // stage ('Source Composition Analysis') {
    //   steps {
    //      sh 'rm owasp* || true '
    //      sh 'wget "https://raw.githubusercontent.com/Mr-Kapil18/cicd-pipeline-project/refs/heads/main/owasp-dependency-check.sh" '
    //      sh 'chmod +x owasp-dependency-check.sh'
    //      sh 'bash owasp-dependency-check.sh'
    //      sh 'cat /var/lib/jenkins/OWASP-Dependency-Check/reports/dependency-check-report.xml' 
    //   }
    // }

    stage('Build') {
      steps {
        sh 'mvn clean package'
      }
    }

	  stage('Test-SSH') {
  steps {
    sshagent(['tomcat']) {
      sh 'ssh -o StrictHostKeyChecking=no kapil@192.168.5.129 "hostname && whoami"'
    }
  }
}
	stage('Deploy-To-Tomcat') {
		steps {
            sshagent(['tomcat']) {
                sh 'scp -o StrictHostKeyChecking=no target/*.war kapil@192.168.5.129:/opt/tomcat/webapps/webapp.war'
                }
            }
        }
  }
}


   
   // stage('OWASP Dependency-Check Vulnerabilities') {
   //   steps {
   //     dependencyCheck additionalArguments: ''' 
   //                 -o './'
   //                 -s './'
   //                 -f 'ALL' 
   //                 --prettyPrint''', odcInstallation: 'OWASP Dependency-Check Vulnerabilities'
        
   //     dependencyCheckPublisher pattern: 'dependency-check-report.xml'
   //   }
   // }
    
  
  //stage ('Static analysis') {
  //  steps { 
  //    withSonarQubeEnv('sonar') {
  //      sh 'mvn sonar:sonar'
	//sh './sonarqube_report.sh'
//        }
//      }
//    }
	  
   

	 //stage ('Dynamic analysis') {
     //       steps {
     //      sshagent(['zap']) {
     //           sh 'ssh -o  StrictHostKeyChecking=no ubuntu@44.202.238.69 "sudo docker run -t owasp/zap2docker-stable zap-full-scan.py -t http://3.83.33.221:8080/webapp" '
		   // sh 'ssh -o  StrictHostKeyChecking=no ubuntu@3.91.196.22 "sudo docker run -t owasp/zap2docker-stable zap-baseline.py -t http://44.203.175.196:8080/webapp" '
		//sh 'ssh -o  StrictHostKeyChecking=no ubuntu@65.1.84.186 "sudo ./zap_report.sh"'
           //   }      
           //}   	  
	  
//}
//}
//}
