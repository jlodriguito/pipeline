pipeline {
    agent { 
	docker {
		image 'ruby:2.4.1' 
		args  '-v /var/lib/jenkins/workspace/pipetest:/app -p 8082:8082'
		reuseNode true
		}
	}
        stages {
   	     stage('build') {
        	    	steps {
               			sh 'bundle'
           		 }
       		 }
     		stage('deploy') {
            		steps {
                		sh 'ruby web.rb -o 0.0.0.0 -p 8082 &'
           		 }
		}
        	stage('test') {
       			steps {
                		sh 'curl -i http://localhost:8082'
            		}
		}
		post {
     			always {
            			junit 'build/reports/**/*.xml'
       			 }
   		 }
	
        }
}
