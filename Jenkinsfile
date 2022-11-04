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
        sh "ansible-playbook Ansible/build.yml -i Ansible/inventory/host.yml"
        }
      }
    }
  }
}
