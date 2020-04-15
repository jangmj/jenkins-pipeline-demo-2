pipeline {
	agent none
    options {
        skipStagesAfterUnstable()
    }
    stages {
        stage('Build') {
		     agent {
		        docker {
		            image 'maven:3-alpine'
		            args '-v /var/jenkins_home/.m2:/root/.m2 -u 1000'
		        }
		    }
            steps {
                sh 'echo "Hello World"'
                sh 'mvn --version'
                sh '''
                    echo "Multiline shell steps works too"
                    id
                    ls -lah
                '''
            	sh 'chmod +x ./jenkins/scripts/deliver.sh'
                sh 'sh ./jenkins/scripts/deliver.sh'
            }
        }
        stage('Deploy') {
        	agent any
            steps {
                sh 'echo "scp Jenkinsfile"'
                sh '''
                	id
                	pwd
                    echo "${CMD}"
                    ls -lah
                    #docker container exec my-maven-project ls
                    #which scp
                    scp -P 22000 /var/jenkins_home/workspace/jenkins-pipeline-demo-2_master/hello.txt webdev@1.242.216.122:~/projects/lotte/
                '''
            }
        }
    }
}