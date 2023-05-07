pipeline{

agent any

stages{

stage('Checkout'){

steps{

git branch: "main", url: 'git repo link' // from where the jenkins files will be

}

}

stage('Build'){

steps{

sh 'chmod a+x mvnw'

sh './mvnw clean package -DskipTests=true'

}

post{

always{

archiveArtifacts 'target/*.jar'

}

}

}

stage('DockerBuild') {

steps {

sh 'docker build -t repo-name/<image-name>:<tag-name> .'

}

}

stage('Login') {

steps {

sh 'echo <dockerhub-password> | docker login -u <dockerhub-username> --password-stdin'

}

}

stage('Push') {

steps {

sh 'docker push <image-name>'

}

}

}

post {

always {

sh 'docker logout'

}

}

}




// This is a Jenkins pipeline script that defines a continuous integration and delivery (CI/CD) pipeline for a Java application.
//  Here is a breakdown of the different stages in this pipeline:

// Checkout: This stage checks out the code from a GitHub repository specified by the url parameter and the branch parameter.
//  Build: This stage builds the application using the Maven wrapper (mvnw) script.The clean option deletes any previously generated build artifacts, 
// and package generates a new build artifact (.jar file) for the application.

// The -DskipTests=true option skips running tests during the build process to save time.The post section archives the build artifact (target/.jar) so that it can be downloaded later.
// DockerBuild: This stage builds a Docker image of the application using the Dockerfile located in the current directory (.) and tags it with the name repo-name/<image-name>:<tag-name>.
// Login: This stage logs in to the Docker registry with the specified username and password.
// Push: This stage pushes the Docker image to the Docker registry with the name repo-name/<image-name>
// post: This section contains a sh step that logs out of the Docker registry.

// The always blocks are executed regardless of the outcome of the previous stage, so in this case,
//  it ensures that the Docker client is logged out after the pipeline is complete.