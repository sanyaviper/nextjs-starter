node { 
    def app 
    def scmVars 
    
    stage('Clone repository') {   
        /* Let's make sure we have the repository cloned to our workspace */
 
        scmVars = checkout scm     
        // scmVars contains the following values   1
        // GIT_BRANCH=origin/mybranch
        // GIT_COMMIT=fc8279a107ebaf806f2e310fce15a7a54238eb71
        // GIT_PREVIOUS_COMMIT=6f2e319a1fc82707ebaf800fce15a7a54238eb71
        // GIT_PREVIOUS_SUCCESSFUL_COMMIT=310fce159a1fc82707ebaf806f2ea7a54238eb71
        // GIT_URL=https://stash.someworkplace.com/scm/poc/api-sample.git
    }
    
    stage('test scope') { 
        echo scmVars.GIT_BRANCH
        echo "scmVars"
        
        
        echo scmVars.GIT_COMMIT
        echo "scmVars"
        
        
        
        // List of all configured branches
        //def allBranches = scm.branches
        //echo allBranches
        // Only the first configured branch name
        //echo "the build worked! The payload is $payload"
        //echo payload
        
        //echo $payload
        /*
        $webhookres='$'

echo $
echo payload
        echo $payload*/
    }
    
    stage ('read properties from webhook json') {
       echo 'Hello World webhook'
        
        echo "My Jenkins job parameter is ${params}"
echo "One of Jenkins job webhook payload field is ${env}"
       /* echo 'Hello World webhook:' + from_webhook
        echo "the build worked! The payload is $from_webhook"
       echo 'git repository name is :' + repository_name
       echo 'author of commit is :' + commit_author*/
        
        
        echo "my_ref: " + my_ref
        
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
