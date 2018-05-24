pipeline { 
    agent {
        //label 'maven||master'
        label 'master'
    }
    tools { 
        maven 'Maven 3.3.9' 
        jdk 'jdk8' 
    }
    stages { 
        stage ('Initialize') {
            steps {
                sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
                ''' 
            }
        }
        stage('Build') { 
            steps { 
               sh 'mvn -Dmaven.test.failure.ignore=true -f complete/pom.xml install'
            }
            post {
                success {
                    archiveArtifacts artifacts: 'complete/target/**/*.jar', fingerprint: true
                    junit 'complete/target/surefire-reports/**/*.xml' 
                }
            }
        }
    }
}
