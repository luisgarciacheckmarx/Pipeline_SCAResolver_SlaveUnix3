pipeline {
    agent { label 'MyLinux' }

    stages {
        
        stage('SCM') {
            steps {
                //sh 'sudo apk add --no-cache git'
                sh 'mvn --version'
                sh 'ls'
		checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/luisgarciacheckmarx/Pipeline_SCAResolver_SlaveUnix3']]]	);
            }
        }
        


		
	stage('SCA Resolver') {
            steps {
		script {
			sh 'rm -f *.pdf'
			//sh '[ -e *.pdf ] && rm *.pdf '
			def tempDir = pwd(tmp: true)
			dir(tempDir) {
				sh 'wget https://sca-downloads.s3.amazonaws.com/cli/1.7.3/ScaResolver-linux64.tar.gz -O ScaResolver.tar.gz'
                        	sh 'tar -xzvf ScaResolver.tar.gz'
                        	sh 'rm -rf ScaResolver.tar.gz'
                        	sh 'chmod +x ScaResolver'
                        	sh 'echo "Current directory: $(pwd)"'
                        	sh 'ls -latr $(pwd)'
				sh './ScaResolver -a ps-team-emea -u luis.garciaviejo@checkmarx.com -p CxPass123! -s /home/jenkins/workspace/Pipeline_SCAResolver_SlaveUnix2 --report-path /home/jenkins/workspace/Pipeline_SCAResolver_SlaveUnix2 --report-type Risk --report-extension Pdf,Json,Xml -n Pipeline_SCAResolver_SlaveUnix2 --bypass-exitcode'
						
				}
			}
            	}
	}
        
        
	stage('Publish as HTML') {
            steps {
		sh 'echo "<html> <body> <h1> Heading HTML test </h1> </body> <html>"'
                //sh 'cat ${JENKINS_HOME}/jobs/${JOB_NAME}/builds/${BUILD_NUMBER}/log >> log.html'
                //sh 'echo "<!DOCTYPE html>" > log.html'
                //sh 'echo "<!DOCTYPE html>" >> log.html'
                
                //sh 'echo "<embed src=/home/jenkins/workspace/Pipeline_SCAResolver_SlaveUnix2/SCA_RiskReport_3f3939dc-4ba8-43ac-878c-774e8eb702e1.pdf width=1500px height=2100px />" > log.html'
                //sh 'cat log.html'
                //sh 'echo "<html> <body> <h1> Heading HTML test </h1> </body> <html>" > log.html'
                //sh 'echo "<html> <body> <h1> Heading HTML test </h1> <embed src=/home/jenkins/workspace/Pipeline_SCAResolver_SlaveUnix2/SCA_RiskReport_3f3939dc-4ba8-43ac-878c-774e8eb702e1.pdf width=1500px height=2100px /> </body> <html>" > log.html'
                //sh 'echo "hola perola adios " >> log.html'
                //sh 'cat SCA_RiskReport_65c882c5-972a-44ad-bbe8-5bdf36ce6ba4.pdf >>log.html'
                //SCA_RiskReport_65c882c5-972a-44ad-bbe8-5bdf36ce6ba4.pdf


                sh 'ls -latr '
                publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: true, reportDir: '.', reportFiles: '*.pdf', reportName: 'SCA scan report', reportTitles: ''])
            }
	}
		
    }
}
