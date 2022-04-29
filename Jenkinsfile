pipeline{
	//agent{docker{image 'maven:3.6.3}}  ---means you want to build inside a Maven image,jenkins will pull image and run the build inside it
	//u can use node:13.8 etc
    agent any
	environment {
		dockerHome = tool 'myDocker'
		mavenHome  = tool 'myMaven'
		PATH ="$mavenHome/bin:$PATH"
		// PATH ="$dockerHome/bin:$mavenHome/bin:$PATH"
	}
    stages{

        stage('Continuous Build'){
			steps{
				//sh 'mvn --version'
				// sh "docker version"
              echo "Download"
			  echo "PATH -$PATH"
			  echo "BUILD_NUMBER - $env.BUILD_NUMBER"
			  echo "BUILD_ID - $env.BUILD_ID"
			  echo "JOB_NAME - $env.JOB_NAME"
			  echo "BUILD_TAG - $env.BUILD_TAG"
			  echo "BUILD-URL -$env.BUILD_URL"

		    }
		}
            
       stage('Package'){

		steps{
            // sh "mvn package"

			}

        }
       
       
	 stage('Build Docker Image'){

			steps{
				echo "build image"
           // "docker build -t shokunbi/docker-image:$env.BUILD_TAG"
		//    script{
		// 	   dockerImage=docker.build{"shokunbi/docker-image:$env.BUILD_TAG"}
		//    }

			}

        }

	   stage('Push Docker Image'){
		   steps{
           script{
			   docker.withRegistry('','dockerhub') {
				 dockerImage.push();
			   	 dockerImage.push('latest');

			   }
			

		   }

			}

        }
    }
	
}
