pipeline {
    agent any
//     options {
//         timeout(time: 1, unit: 'HOURS') 
//     }
    stages {       
//             stage("QA"){
//                 steps {
//                     echo "Running QA"
//                     withSonarQubeEnv('SonarCloud') {
//                         sh "mvn sonar:sonar"
//                 }
                
//               }
//             }
            stage("QG") {
                steps {
                       // timeout(time: 1, unit: 'HOURS')
                        script {
                            define qg = waitForQualityGate()
                            if (qg.status != 'OK') {
                                error "Pipeline aborted due to failure: ${qg.status}"
                            }
                        }
                    }
                }
            }
//             steps {
//                 sh 'mvn -B -DskipTests clean package'
//             }
//         }
//         stage('Test') { 
//             steps {
//                 sh 'mvn test' 
//             }
//             post {
//                 always {
//                     junit 'target/surefire-reports/*.xml' 
//                 }
            }
   //     }
 //   }

//}
