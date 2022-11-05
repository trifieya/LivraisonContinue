pipeline
{
  agent any
  stages {
    stage ('Pull'){
      steps{
        script{
            checkout([$class: 'GitSCM', branches: [[name: '*/main']],
                userRemoteConfigs:[[
                    url: 'https://github.com/trifieya/LivraisonContinue.git'
                ]]
            
            ])

        }
      }
    }
    stage ('Build')
    {
      steps {
        script{
        sh "npm install --legacy-peer-deps"
        sh"ansible-playbook Ansible/build.yml -i Ansible/inventory/host.yml"
        }
      }
    }
    
    stage ('docker')
    {
      steps {
        script{
        sh"ansible-playbook Ansible/docker.yml -i Ansible/inventory/host.yml"
        }
      }
    }
    stage('Login') {

      steps {
	sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}
    stage ('docker registry ')
    {
      steps {
        script{
        sh"ansible-playbook Ansible/docker-registry.yml -i Ansible/inventory/host.yml"
        }
      }
    }
    
    
  }
}
