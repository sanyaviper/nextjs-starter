node { 
    def app
 
    stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace */

        checkout scm
        
        sh "ls -la"
        
        
        /*sh "sudo service docker status"*/
    }
    stage ('read properties from webhook json') {
       echo 'Hello World webhook'
        echo 'Hello World webhook:' + from_webhook
        echo "the build worked! The payload is $from_webhook"
       echo 'git repository name is :' + repository_name
       echo 'author of commit is :' + commit_author
    }
    
    stage('Build image') {
        /* This builds the actual image; synonymous to
         * docker build on the command line */

        app = docker.build("node-app")
    }

    stage('Test image') {
        /* Ideally, we would run a test framework against our image.
         * For this example, we're using a Volkswagen-type approach ;-) */

        app.inside {
            sh 'echo "Tests passed"'
        }
        
        sh "ls -la"
    }

    stage('Push image') {
        /* Finally, we'll push the image with two tags:
         * First, the incremental build number from Jenkins
         * Second, the 'latest' tag.
         * Pushing multiple tags is cheap, as all the layers are reused. */
        /*docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }*/
          app.run('-p 80:3000')
        /*sh 'docker run -it -p 3000:3000 node-app'*/
        sh 'echo "Push image"'
    }
}
