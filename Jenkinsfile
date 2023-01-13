pipeline {
    agent any
    stages{

    stage('Clone repository') {
        steps{
            script{
                checkout scm
            }
        }
      

    }

    stage('Update GIT') {
        steps{

        
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        sh "git config user.email vishal.sader@testingxperts.com"
                        sh "git config user.name VishalTx"
                        //sh "git switch master"
                        sh "cat deployment.yaml"
                        sh "sed -i 's+vishal7500/sader.*+vishal7500/sader:${DOCKERTAG}+g' deployment.yaml"
                        sh "cat deployment.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/kubernetesmanifest.git HEAD:main"
                        
      }
    }
  }
}
    }
    
    //              withKubeConfig([credentialsId: 'kubernetes_updated', configs: 'deployment.yaml'])
    stage('deploy to k8s'){
            steps{
                withKubeConfig(caCertificate: '', clusterName: '', contextName: '', credentialsId: 'K8SL', namespace: '', restrictKubeConfigAccess: false, serverUrl: '') {
    // some block
                    sh "/var/lib/jenkins/workspace/kubectl apply -f deploymentservice.yaml"
}
    }
}
    }
}

   



            
