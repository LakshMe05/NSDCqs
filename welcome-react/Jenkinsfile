pipeline {
    agent any
    environment {
        IMAGE_NAME = "react-app"
        CONTAINER_NAME = "cranky_kirch"
    }

    tools {
        nodejs 'NodeJS-20.19.6'
    }

    stages {
        stage('Clone Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/LakshMe05/NSDCqs.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                dir('welcome-react') {
                    sh 'npm install'
                }
            }
        }

        stage('Build React App') {
            steps {
                dir('welcome-react') {
                    sh 'npm run build'
                }
            }
        }
        stage('Build Docker Image') {
            steps {
                // Use $IMAGE_NAME instead of %IMAGE_NAME%
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Stop Old Container') {
            steps {
                sh '''
                docker stop $CONTAINER_NAME || exit 0
                docker rm $CONTAINER_NAME || exit 0
                '''
            }
        }

        stage('Run Docker Container') {
            steps {
                sh '''
                docker run -d -p 5173:5173 --name $CONTAINER_NAME $IMAGE_NAME
                '''
            }
        }
    }

    post {
        success {
            echo 'React build successful 🎉'
        }
        failure {
            echo 'Build failed ❌'
        }
    }
}
// pipeline {
//     agent any

//     environment {
//         IMAGE_NAME = "react-vite-app"
//         CONTAINER_NAME = "react-vite-container"
//     }

//     stages {

//         stage('Clone Code') {
//             steps {
//                 git branch: 'main',
//                     url: 'https://github.com/MamthaKSunilkumar/CS8_demo.git'
//             }
//         }

//         stage('Build Docker Image') {
//             steps {
//                 bat 'docker build -t $IMAGE_NAME .'
//             }
//         }

//         stage('Stop Old Container') {
//             steps {
//                 bat '''
//                 docker stop $CONTAINER_NAME || true
//                 docker rm $CONTAINER_NAME || true
//                 '''
//             }
//         }

//         stage('Run Docker Container') {
//             steps {
//                 bat '''
//                 docker run -d \
//                 -p 5173:5173 \
//                 --name $CONTAINER_NAME \
//                 $IMAGE_NAME
//                 '''
//             }
//         }
//     }

//     post {
//         success {
//             echo 'React app deployed using Docker successfully 🎉'
//         }
//         failure {
//             echo 'Deployment failed ❌'
//         }
//     }
// }
