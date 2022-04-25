pipeline {
    agent any
    stages {
        stage('Build') {
            
            stage("QA"){
                steps {
                    echo "Running QA"
                    withSonarQubeEnv('') {
                        bat"mvn sonar:sonar"
                }
                
              }
            }
            stage("QG") {
                steps {
                    timeout(time, unit:'HOURS') {
                        script {
                            define qg = waitForQualityGate()
                            if (qg.status != 'OK') {
                                error "Pipeline aborted due to failure: ${qg.status}
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
        }
    }
}
