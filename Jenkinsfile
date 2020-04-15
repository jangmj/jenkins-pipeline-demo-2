pipeline {
    agent {
        docker {
            image 'maven:3-alpine'
            args '-v /var/jenkins_home/.m2:/root/.m2 -u 1000'
        }
    }
    options {
        skipStagesAfterUnstable()
    }
    stages {
        stage('Build') {
            steps {
                sh 'echo "Hello World"'
                sh 'mvn --version'
                sh '''
                    echo "Multiline shell steps works too"
                    id
                    ls -lah
                '''
            }
        }
        stage('Deploy') {
            steps {
            	sh 'chmod +x ./jenkins/scripts/deliver.sh'
                sh 'sh ./jenkins/scripts/deliver.sh'
                sh 'echo "scp Jenkinsfile"'
                sh '''
                	id
                	pwd
                    echo "${CMD}"
                    ls -lah
                    #docker container exec my-maven-project ls
                    #which scp
                    scp -P 22000 ./hello.txt webdev@1.242.216.122:~/projects/lotte/
                '''
            }
        }
    }
}