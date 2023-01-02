node {

    def mvnHome = tool 'maven-3.5.2'
    def dockerImage
    def dockerImageTag = "app${env.BUILD_NUMBER}"

    stage('Clone Repo') {
      echo "Clone Repo from a GitHub repo"

      checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'my_github', url: 'https://github.com/denisxtiawan/repo_for_cicd_springboot']])

      mvnHome = tool 'maven-3.5.2'
    }

    stage('Build Project') {
      echo "build project via maven"
      sh "'${mvnHome}/bin/mvn' clean install"
    }

    stage('Build Docker Image') {

      echo "Build docker image"
      sh "ls -lrt"
      sh "docker image build -t app:${env.BUILD_NUMBER} . "
      sh "docker images"

    }


    stage('Deploy Docker Image'){
      echo "Deploy docker image"

	  // run if this container is exist
	  // sh "docker stop restapi-springboot-mysql"
	  // sh "docker rm restapi-springboot-mysql"

      // create and run container
	  sh "docker run  --detach  --name docker_spring_app  --publish 8181:8181 --network=docker_spring_network  -e APP_HOST=spring_docker_app   -e APP_PORT=8181 -e APP_DB_HOST=docker_spring_mysql -e APP_DB_PORT=3300  -e APP_DB_USER=user -e APP_DB_PASSWORD=password -e APP_DB_NAME=database app:${env.BUILD_NUMBER}"

	  // -e APP_HOST=spring_docker_app   -e APP_PORT=8181 -e APP_DB_HOST=docker_spring_mysql -e APP_DB_PORT=3300  -e APP_DB_USER=user -e APP_DB_PASSWORD=password -e APP_DB_NAME=database

    }


}
