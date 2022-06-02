pipeline {

    agent any
    environment {
    		DOCKERHUB_CREDENTIALS=credentials('1771985')
    	}
    tools {
        maven 'mvn3.8.5'
    }
    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
                sh 'mvn test'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
                sh 'mvn quarkus:add-extension -Dextensions="container-image-docker"'
                sh 'mvn clean package -Dquarkus.container-image.build=true -Dquarkus.container-image.group=mshannah -Dquarkus.container-image.name=test'
            }
        }
        stage('Login') {

        			steps {
        				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
        			}
        		}
        stage('Push') {

        			steps {
        				sh 'docker push mshannah/test:1.0-SNAPSHOT'
        			}
        		}
    }
    post {
    		always {
    			sh 'docker logout'
    		}
    	}

}