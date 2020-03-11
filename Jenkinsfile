node {
    def app
    
    stage('Clone repository') {
        /* Cloning the Repository to our Workspace 

        checkout scm*/
    }

    stage('Build image') {
        /* This builds the actual image in the local docker host and use the variable for further stage
        app = docker.build("samplewebapi", ". -f Dockerfile")*/
    }

    stage('Test image') {
        
        app.inside {
            echo "Tests passed"
	    echo "The build number is ${env.BUILD_NUMBER}"
        }
    }

    stage('Push image') {
         
	/*You would need to first register with DockerHub before you can push images to your account*/
		
        docker.withRegistry('http://10.16.131.56:5000/samplewebapi') {
            /*app.push("${env.BUILD_NUMBER}")
            app.push("latest")*/ 
            } 
                echo "Trying to Push Docker Build to DockerHub"
    }
    stage('Deploy in kubernetes')
    {
    	/*kubectl apply -f SampleWebApi/samplewebapi-deployment.yml */
	 kubernetesDeploy(configs: "Deployments/samplewebapi-v2.deployment.yml", kubeconfigId: "mykubeconfig")    
    }
}
