pipeline {
    agent any
         stages{
    
    stage ('git clone') {
            steps {
        echo "code is building"
         git 'https://github.com/umahari/testing.git'
            }
        }

        stage ('Bulding docker docker image') {
            steps {
                echo "build docker image"
                sh 'docker build --no-cache -t saidevops94/repos .'
            }
        }
        stage ('Uploading to docker hub') {
            steps {
                echo "uploading to docker hub" 
                sh 'docker login -u saidevops94 -p Sai@809969'
                sh 'docker push saidevops94/repos:latest'
            }
        }

        stage ('deploying to GKE') {
           steps {
                echo "deploying imges to GKE"
                sh 'kubectl apply -f test-dep.yaml'
                sh 'kubectl set image deployment/httpd-deployment httpd2=saidevops94/repos:latest'
                sh 'kubectl apply -f test-svc.yaml'
                sh 'kubectl rollout restart deployment/httpd-deployment'
                sh 'docker rmi -f $(docker images --filter "dangling=true" -q --no-trunc)'
               
           }
    }  
        
}

}
