node {
    docker.image ('maven:latest').inside('-v /root/.m2:/root/.m2') {
               
            stage('Build') {
                sh 'mvn -B -DskipTests clean package'
            }
        
            stage('Test') {
                sh 'mvn test'
                junit 'target/surefire-reports/*.xml'
            }

        if (currentBuild.currentResult == 'SUCCESS') {
            stage('Deliver') {
                sh './jenkins/scripts/deliver.sh'
            }    
        }
    }
}
