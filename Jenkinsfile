pipeline {
  agent any
    stages {
        stage('Pull') {
             steps{
                script{
                    checkout([$class: 'GitSCM', branches: [[name: '*/master']],
                        userRemoteConfigs: [[
                            credentialsId: '6aaaa85f-9a56-4529-8c55-b339e135ce05',
                            url: 'https://github.com/jkhazri/MyappV2.git']]])
                }
            }
        }
   	stage('Install') {
             steps{
                script{
                    sh "npm install"
                }
            }
        }

	stage ('Build') {
	
			steps {
			
			sh "ansible-playbook Ansible/build.yml -i Ansible/inventory/host.yml"
			}


	}




	//stage('ng Build') {
          //   steps{
             //   script{
           //         sh "sudo ng build"
                //}
          //  }
     //   }

	stage('Docker') {
             steps{
                script{
                    sh "sudo ansible-playbook Ansible/docker.yml -i Ansible/inventory/host.yml"
                }
            }
        }
         stage('DockerHub push') {
             steps{
                script{
                    sh "ansible-playbook Ansible/docker-registry.yml -i Ansible/inventory/host.yml"
                }
            }
        }

}}	
