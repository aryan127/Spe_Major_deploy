pipeline {
  agent any

  stages {
    stage('Git Back end') {
        environment {
              IMAGE_NAME=''
        }
        steps {
            git url: 'https://github.com/aryan127/placement-backend.git' 
            script {
                IMAGE_NAME=docker.build "aryan1207/spe_backend"
                docker.withRegistry('','docker-key'){
                IMAGE_NAME.push()
            }
          
          }
        }
    }
    stage('Git Front end') {
        environment {
                IMAGE_NAME=''
        }
        steps {
            git url: 'https://github.com/aryan127/placement.git'
            script {
            IMAGE_NAME=docker.build "aryan1207/spe_frontend"
            docker.withRegistry('','docker-key'){
                IMAGE_NAME.push()
            }
          }
        }
    }

    stage('Deploy with Ansible') {
      steps {
        script{
          sh 'ansible-playbook ansible/deploy.yml -i ansible-deploy/inventory --user aryan '
        }
      }
    }
  }
}