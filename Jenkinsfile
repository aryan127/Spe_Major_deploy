// pipeline {
//   agent any

//   stages {
//     stage('Git Back end') {
//         environment {
//               IMAGE_NAME=''
//         }
//         steps {
//             git url: 'https://github.com/aryan127/placement-backend.git' 
//             script {
//                 IMAGE_NAME=docker.build "aryan1207/spe_backend"
//                 docker.withRegistry('','docker-key'){
//                 IMAGE_NAME.push()
//             }
          
//           }
//         }
//     }
//     stage('Git Front end') {
//         environment {
//                 IMAGE_NAME=''
//         }
//         steps {
//             git url: 'https://github.com/aryan127/placement.git'
//             script {
//             IMAGE_NAME=docker.build "aryan1207/spe_frontend"
//             docker.withRegistry('','docker-key'){
//                 IMAGE_NAME.push()
//             }
//           }
//         }
//     }

//     stage('Deploy with Ansible') {
//       steps {
//         script{
//           sh 'ansible-playbook ansible/deploy.yml -i ansible-deploy/inventory --user aryan '
//         }
//       }
//     }
//   }
// }

pipeline {
    agent any

    environment {
        IMAGE_NAME=''
    }

    stages {
        stage('Clone configuration repository') {
            steps {
                checkout([$class: 'GitSCM', 
                          branches: [[name: '*/master']], 
                          userRemoteConfigs: [[url: 'https://github.com/aryan127/Spe_Major_deploy.git']]])
            }
        }

        stage('Build and push frontend image') {
            steps {
                checkout([$class: 'GitSCM', 
                          branches: [[name: '*/master']], 
                          userRemoteConfigs: [[url: 'https://github.com/aryan127/placement.git']]])

                script {
                    IMAGE_NAME=docker.build "aryan1207/spe_frontend"
                    docker.withRegistry('','78893db7-6f42-48c4-8959-fe97266d632a'){
                      IMAGE_NAME.push()
                    }
                }
            }
        }

        stage('Build and push backend image') {
            steps {
                checkout([$class: 'GitSCM', 
                          branches: [[name: '*/master']], 
                          userRemoteConfigs: [[url: 'https://github.com/aryan127/placement-backend.git']]])

                script {
                    IMAGE_NAME=docker.build "aryan1207/spe_backend"
                    docker.withRegistry('','78893db7-6f42-48c4-8959-fe97266d632a'){
                      IMAGE_NAME.push()
                    }
                }
            }
        }

        stage('Deploy application using Ansible') {
            steps {
                sh "cd /home/aryan/Desktop/Placement/Spe_Major_deploy/ansible && ansible-playbook /home/aryan/Desktop/Placement/Spe_Major_deploy/ansible/deploy.yml -i /home/aryan/Desktop/Placement/Spe_Major_deploy/ansible/inventory"
            }
        }

    }
}