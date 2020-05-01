pipeline {
   agent any
   
   environment {

        PATH = '/usr/local/bin:/usr/bin:/bin:/usr/local/games:/usr/games:/usr/local/go/bin'
        GOPATH = '/var/lib/jenkins/workspace/gogit'
    }


   stages {
    stage('Hello') {
         steps {
            echo 'Hello World'
         }
    }
    stage('Print environment vars') {
        steps {
            echo "PATH is: ${PATH}"
            echo "GOPATH is: ${GOPATH}"
            sh "printenv"
        }
    }
    stage('Download source') {
        steps {
            //sh "rm -rf /root/.jenkins/workspace/gogit/*"
            deleteDir()
            echo 'Cleaning up workspace directory'
            //sh "cd /root/.jenkins/workspace/"
            //sh "git clone https://github.com/benpinter88/gogit.git"
            git 'https://github.com/benpinter88/gogit'
            echo 'Downloading source from git'
        }
    }
    stage('Build source') {
        steps{
            echo 'Building Executable'
            sh "cd /var/lib/jenkins/workspace/gogit"
            echo 'Go Env.'
            sh "go env"        
            //sh "go build hello.go"
            //sh "./hello"
            //sh "cat hello.go"
            echo 'Contents of workspace directory:'
            //pwd()
            //sh "ls -lha"
            sh "pwd && ls -lha"
            echo 'Build hello.go'
            sh "go build hello.go"
            echo 'Running compiled executable:'
            sh "./hello"
            //invoke bauxit's riot reporter executable
            //sh "ln -s /root/.jenkins/riot-reporter/riot-reporter /root/.jenkins/workspace/gogit/riot-reporter"
            //sh "JENKINS_MESSAGE=build_successful ./riot-reporter"
            
        }
        
    }
    stage('Build Docker image') {
        steps{
            echo 'Building Docker image'
            //pwd()
            sh "pwd"
            sh "touch Dockerfile"
            //sh "echo -e 'FROM alpine COPY hello /var/hello CMD /var/hello > /var/hello.txt && HELLO=$(cat /var/hello.txt) && echo $HELLO' >> Dockerfile"
            sh label: '', script: 'echo -e \'FROM alpine COPY hello /var/hello CMD /var/hello > /var/hello.txt && HELLO=$(cat /var/hello.txt) && echo $HELLO\' >> Dockerfile'
	    sh "cat Dockerfile"
	
        }
    }
    stage('Run Docker image'){
		steps{
		sh label: '', script: 'docker run --rm benpinter88/hellotest'
		}
	}
  }
}
