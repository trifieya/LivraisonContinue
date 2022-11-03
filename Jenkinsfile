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
        sh "ansible-playbook ansible/build.yml -i ansible/inventory/host.yml"
        }
      }
    }
  }
}
