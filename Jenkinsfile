pipeline {

    agent any

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