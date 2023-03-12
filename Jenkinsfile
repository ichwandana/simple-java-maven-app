node {
    docker.image ('maven:latest').inside('-v /root/.m2:/root/.m2') {
               
            stage('Build') {
                sh 'mvn -B -DskipTests clean package'
            }
        
            stage('Test') {
                sh 'mvn test'
                junit 'target/surefire-reports/*.xml'
                input message: 'Lanjutkan ke tahap Deploy'
               

            }

        if (currentBuild.currentResult == 'SUCCESS') {
            stage('Deploy') {
                sh './jenkins/scripts/deliver.sh'
                sleep 60                               
            }    
        }
    }
}
