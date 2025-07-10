pipeline {
    agent any

    stages {
        stage("build") {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                    sh 'docker build -t webapp:v${BUILD_NUMBER} .'
                    sh 'docker tag webapp:v${BUILD_NUMBER} mouner0x/webapp:v${BUILD_NUMBER}'
                    sh 'echo $PASS | docker login -u $USER --password-stdin'
                    sh 'docker push mouner0x/webapp:v${BUILD_NUMBER}'
                }
            }
        }

        stage("deploy") {
            steps {
                sh 'docker run -it -d -p 300${BUILD_NUMBER}:8080 mouner0x/webapp:v${BUILD_NUMBER}'
            }
        }
    }
}
