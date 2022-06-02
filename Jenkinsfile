pipeline {

    agent {
            docker {
                image 'maven:3.8.1-adoptopenjdk-11'
                args '-v /root/.m2:/root/.m2'
            }
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
    }
}