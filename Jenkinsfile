pipeline {
    agent { 
	docker {
		image 'ruby:2.4.1' 
		args  '-v /var/lib/jenkins/workspace/pipetest:/app -p 8083:8083'
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
                		sh 'ruby web.rb -o 0.0.0.0 -p 8083 &'
           		 }
		}
        	stage('test') {
       			steps {
				sh 'sleep 10'
                		sh 'curl -i http://localhost:8083 >> output.txt'
            		}
		}
	
        }
	post {
        	always {
			archiveArtifacts artifacts: 'output.txt' , fingerprint: true
			sh 'curl -i http://localhost:8082 >> output.txt'
        	}
   	}
}

