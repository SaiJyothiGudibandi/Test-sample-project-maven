pipeline {
   agent any
       parameters {
           string(name: 'testVarJob', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
           }

   stages {
      stage('Clone') {
         steps {
      // Get some code from a GitHub repository
          checkout scm
         }
      }
      stage('Build') {
         steps {
            // Run Maven on a Unix agent.
            sh "mvn web3j:generate-sources"
            echo "--------Testing parameterized feature---------"
            sh "echo ${params.testVarJob}"
            sh "echo $Git_URL"


            // To run Maven on a Windows agent, use
            // bat "mvn -Dmaven.test.failure.ignore=true clean package"
         }
      }
      stage('docker build') {
         steps {
             sh "docker build -t=saijyothi9/nginx ."
         }
      }
       stage('docker push') {
         steps {
             sh "docker push saijyothi9/nginx"
         }
      }
       stage('docker run ') {
         steps {
             sh "docker stop \$(docker ps -a -q)"
			 sh "docker rm \$(docker ps -a -q)"
             sh "docker run --name mynginx1 -p 80:80 -d saijyothi9/nginx"
         }
      }
        
   }
}
