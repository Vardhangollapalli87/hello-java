// pipeline {
//     agent any

//     stages {

//         stage('Checkout Code') {
//             steps {
//                 echo 'Code checked out from Git'
//             }
//         }

//         stage('Compile Java') {
//             steps {
//                 sh '''
//                     rm -rf build
//                     mkdir build
//                     javac -d build src/Hello.java
//                 '''
//             }
//         }

//         stage('Create Executable JAR') {
//             steps {
//                 sh '''
//                     jar cfe hello.jar Hello -C build .
//                 '''
//             }
//         }
//     }

//     post {
//         success {
//             archiveArtifacts artifacts: '*.jar'
//         }
//     }
// }

// pipeline {
//     agent any


//     stages {

//         stage('Checkout Code') {
//             steps {
//                 echo 'Code already checked out from Git'
//             }
//         }

//     stage('Compile Java') {
//         steps {
//             sh '''
//                 rm -rf build
//                 mkdir build
//                 javac -d build src/Hello.java
//                 jar cfe hello.jar Hello -C build .
//             '''
//         }
//     }


//         stage('Prepare Package Directory') {
//             steps {
//                 sh '''
//                     mkdir -p package/usr/local/bin
//                     cp hello.jar package/usr/local/bin/
//                 '''
//             }
//         }

//         stage('Build DEB using FPM') {
//             steps {
//                 sh '''
//                     fpm -s dir -t deb -n hello-java -v 1.0.${BUILD_NUMBER} --prefix=/ -C package
//                 '''
//             }
//         }
//     }

//     post {
//         success {
//             archiveArtifacts artifacts: '*.deb'
//         }
//     }
// }



pipeline {
    agent any

    stages {

        stage('Compile Java') {
            steps {
                bat '''
                rmdir /s /q build 2>nul
                mkdir build

                javac -d build src\\Hello.java
                jar cfe hello.jar Hello -C build .
                '''
            }
        }

        stage('Prepare Package Directory') {
            steps {
                bat '''
                rmdir /s /q package 2>nul
                mkdir package\\usr\\local\\bin
                copy hello.jar package\\usr\\local\\bin\\
                '''
            }
        }

        stage('Build DEB using FPM') {
            steps {
                bat '''
                fpm -s dir -t deb ^
                 -n hello-java ^
                 -v 1.0.%BUILD_NUMBER% ^
                 --architecture all ^
                 -C package
                '''
            }
        }
    }

    post {
        success {
            archiveArtifacts artifacts: '*.deb'
        }
    }
}


