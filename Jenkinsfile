pipeline {

  environment {
    label = "dev-deploy-mobile-web-app"
    namespace = "dev"
    environ = "dev"
  }
  agent any

    stages {

      stage ('Checkout SCM'){
        steps {
          checkout([$class: 'GitSCM', branches: [[name: '*/dev']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'git', url: 'https://github.com/rohan4linux/mobile-web-app-deployments.git']]])
        }
      }
	  
	  stage ('Deploy Helm Charts')  {
	      steps {
           sh "sudo /bin/helm version"
          
           dir("iwayq-web-app"){
                    sh 'pwd'
                    sh "sudo /bin/helm repo add mobile-local https://valaxytech529.jfrog.io/artifactory/mobile-helm-local --username rohan.reddy529@gmail.com --password 4getmenot@J"
                    sh "sudo /bin/helm repo update"
                    sh "sudo /bin/helm upgrade iwayq-web-app-${environ} --install --namespace ${namespace}  --force ."
                    sh "sudo /bin/helm list -a --namespace ${namespace}"
                }
        }
         
      }
         
   } 
}