pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                echo 'Code checked out from Git'
            }
        }

        stage('Compile Java') {
            steps {
                sh '''
                    rm -rf build
                    mkdir build
                    javac -d build src/Hello.java
                '''
            }
        }

        stage('Create Executable JAR') {
            steps {
                sh '''
                    jar cfe hello.jar Hello -C build .
                '''
            }
        }
    }

    post {
        success {
            archiveArtifacts artifacts: '*.jar'
        }
    }
}
