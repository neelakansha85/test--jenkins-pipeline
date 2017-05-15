#!groovy

node('node') {
    currentBuild.result = "SUCCESS"

    try {

       stage('Checkout'){

          checkout scm
       }

       stage('Test'){

         env.NODE_ENV = "test"

         print "Environment will be : ${env.NODE_ENV}"

         sh 'echo This is Test'
         sh 'node -v'
         // sh 'npm prune'
         // sh 'npm install'
         // sh 'npm test'

       }

       stage('Build Docker'){
         sh 'echo This is Build Docker'

            // sh './dockerBuild.sh'
       }

       stage('Deploy'){

         echo 'Push to Repo'
         sh 'echo "./dockerPushToRepo.sh"'

         echo 'ssh to web server and tell it to pull new image'
         // sh 'ssh deploy@xxxxx.xxxxx.com running/xxxxxxx/dockerRun.sh'

       }

       stage('Cleanup'){

         echo 'prune and cleanup'
         // sh 'npm prune'
         // sh 'rm node_modules -rf'

         mail body: 'project build successful',
                     from: 'jenkins@nsdesigners.com',
                     replyTo: 'jenkins@nsdesigners.com',
                     subject: 'project build successful',
                     to: 'neel@nsdesigners.com'
       }



    }
    catch (err) {

        currentBuild.result = "FAILURE"

            mail body: "project build error is here: ${env.BUILD_URL}" ,
            from: 'jenkins@nsdesigners.com',
            replyTo: 'jenkins@nsdesigners.com',
            subject: 'project build failed',
            to: 'neel@nsdesigners.com'

        throw err
    }

}