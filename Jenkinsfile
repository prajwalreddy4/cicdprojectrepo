pipeline{
    agent{
        node{
            label 'JenkinSlaveNodeLabel'
        }
    }

    stages{

        stage("checkout"){

            steps{
                git url:'https://github.com/prajwalreddy4/cicdprojectrepo.git',branch:'main'
            }

        }
        // stage('cleanup stage') { //in docker befour creating new container need to delete previous for latest update
        //     steps {
        //         sh 'docker rmi -f myimagecicdproj'
        //         sh 'docker rm -f $(docker ps -aq)'
        //     }
        // }

        stage("docker image create"){
            steps{
                 sh 'docker build -t myimagecicdproj .'
            }
        }

        stage('Build and Push Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                    // in above line we have given ID and created 2 variables(DOCKER_USERNAME, DOCKER_PASSWORD) using usernameVariable and passwordVariable.
                    sh 'echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin' // echo will take pwd and assign to --password-stdin to avoid printing in pipeling console
                    sh 'docker tag myimagecicdproj $DOCKER_USERNAME/myimagecicdproj'
                    sh 'docker push $DOCKER_USERNAME/myimagecicdproj'// $DOCKER_NAME this varibale value it wil take (linux variable)
                }
                   
            }
        }

         stage('Run Docker Container') {
            steps {
                sh 'kubectl delete deployment my-deployment' // same like docker need to delete old deployment for latest changes
                sh 'docker run -d -p 8501:8501 myimagecicdproj'
            }
        }


    }
}