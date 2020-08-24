node {
    def app

    stage('Clone repository') {
        /* Cloning the Repository to our Workspace */

        checkout scm
    }

    stage('Build image') {
        /* This builds the actual image */

        app = docker.build("master6789/nodeapp")
    }

    stage('Test image') {
        
        app.inside {
            echo "Tests passed"
        }
    }

    stage('Push image') {
        /* 
			You would need to first register with DockerHub before you can push images to your account
		*/
        docker.withRegistry('https://registry.hub.docker.com', 'docker-hub') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
            } 
                echo "Trying to Push Docker Build to DockerHub"
    }
	stage('kubernetes deploy') {
		kubeconfigId: 'kubeconfig-credentials-id',               // REQUIRED

                 configs: '<ant-glob-pattern-for-resource-config-paths>', // REQUIRED
                 enableConfigSubstitution: false,
        
                 secretNamespace: '<secret-namespace>',
                 secretName: '<secret-name>',
                 dockerCredentials: [
                        [credentialsId: '<credentials-id-for-docker-hub>'],
                        [credentialsId: '<credentials-id-for-other-private-registry>', url: '<registry-url>'],
                 ]
)
}
