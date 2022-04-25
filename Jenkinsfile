pipeline {
    agent any
    options {
        timeout(time: 1, unit: 'HOURS') 
    }
    stages {
//         stage('Build') {         
            stage("QA"){
                steps {
                    echo "Running QA"
                    withSonarQubeEnv('SonarCloud') {
                        bat"mvn sonar:sonar"
                        -Dsonar.pullrequest.provider=GitHub \
                        -Dsonar.pullrequest.github.repository=${org}/${repo} \
                        -Dsonar.pullrequest.key=${env.CHANGE_ID} \
                        -Dsonar.pullrequest.branch=${env.CHANGE_BRANCH} \
                }
                
              }
            }
            stage("QG") {
                steps {
                //    timeout(time, unit: 'HOURS') {
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
