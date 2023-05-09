pipeline {
  agent any
  
  tools {
    // specify the Docker pipeline plugin version to use
    dockerTool 'docker'
  }

  environment {
    // define environment variables at the top-level of the pipeline block
    BACKEND_IMAGE_NAME = 'aryan1207/spe_backend'
    FRONTEND_IMAGE_NAME = 'aryan1207/spe_frontend'
  }

  stages {
    stage('Git Back end') {
      steps {
        // clone the repository
        git url: 'https://github.com/aryan127/placement-backend.git'
        // build and push the Docker image to the registry
        script {
          docker.build(BACKEND_IMAGE_NAME).push()
        }
      }
    }
    stage('Git Front end') {
      steps {
        // clone the repository
        git url: 'https://github.com/aryan127/placement.git'
        // build and push the Docker image to the registry
        script {
          docker.build(FRONTEND_IMAGE_NAME).push()
        }
      }
    }
    stage('Deploy with Ansible') {
      steps {
        // execute the Ansible playbook
        sh 'ansible-playbook ansible/deploy.yml -i ansible-deploy/inventory --user aryan'
      }
    }
  }
}

// pipeline {
//   agent any

//   stages {
//     stage('Git Back end') {
//         environment {
//                 IMAGE_NAME=''
//         }
//         steps {
//             git url: 'https://github.com/aryan127/placement-backend.git'   
//         }
//         steps {
//             script {
//                 IMAGE_NAME=docker.build "aryan1207/spe_backend"
//                 docker.withRegistry('','docker-key'){
//                 IMAGE_NAME.push()
//             }
          
//         }


//         }
//     }
//     stage('Git Front end') {
//         environment {
//                 IMAGE_NAME=''
//         }
//         steps {
//             git url: 'https://github.com/aryan127/placement.git'
//         }
//         steps {
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