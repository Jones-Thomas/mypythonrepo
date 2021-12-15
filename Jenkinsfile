pipeline {
    agent any
    environment {
        dockerImage=''
        registry='jonesthomas/mypythonrepo'
        registryCredential = 'dockerhub_test'
    }
    stages{
        stage("Git pull"){
            steps{
            checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Jones-Thomas/mypythonrepo.git']]])
            }
        }
        
        stage("Docker Build"){
            steps{
                script{
                    dockerImage = docker.build registry
                }
            }
        }
        
        stage("DockerHub Push"){
            steps{
                script{
                    docker.withRegistry( '', registryCredential ) {
                        dockerImage.push()
                        
                    }
                    
                }
            }
        }
        stage('Docker stop container') {
            steps {
            sh 'docker ps -f name=mypythonappContainer -q | xargs --no-run-if-empty docker container stop'
            sh 'docker container ls -a -fname=mypythonappContainer -q | xargs -r docker container rm'
            }
            
        }
        stage('Docker Run container') {
        steps {
            script {
                dockerImage.run("-p 5000:5000 --rm --name mypythonappContainer")
            }
        }
        }
        // stage('Cleaning up') { 
        //     steps { 
        //             sh "docker rmi $registry" 
        //         }
        //     } 
    }
}
