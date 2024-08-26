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
        stage("docker image create"){
             sh 'docker build -t myimagecicdproj .'
        }

        /*stage("docker image push to Dockerhub"){
            steps{
              sh 'docker tag myimage1 prajwreddy/myimagecicdprj'
              sh 'docker push prajwreddy/myimagecicdprj'

            }
        }
        */

    }
}