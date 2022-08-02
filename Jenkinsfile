pipeline {

    environment {
        DocImageName = "aswinivunnava/test-axxya"
        DocImage = ""
    }

    agent any

    stages {

        stage('clone github') {
            steps {
                git https://github.com/aswinivunnava/axxya-test.git
            }
        }
        stage('build a docker image'){
            steps {
                script {
                    docImage = docker.build DocImageName
                }
            }
        }
        stage ('pushing image') {
            environment {
                registryCredientials = 'dockerHubLogin'
            }
            steps {
                script {
                    docker.withRegistry ('https://registry.hub.docker.com' , registryCredientials ) {
                        docImage.push ("latest")
                    }
                }
            }
        }
        stage ('Deploying to kubernetes') {
            steps {
                script {
                    kubernetesDeploy (configs: "kubdeploymentService.yml" , kubeconfigID: "kubernetes")
                }
            }
        }


        

        
    }
}