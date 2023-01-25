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
      //sh "'${mvnHome}/bin/mvn' clean install -o"
      sh "'${mvnHome}/bin/mvn' clean install "
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
	  // sh "docker stop restapi_springboot_mysql"
	  // sh "docker rm restapi_springboot_mysql"

      // create and run container
	  sh "docker run  --detach  --name restapi_springboot_mysql  --publish 1234:1234 --network=server_network  -e APP_HOST=restapi_springboot_mysql   -e APP_PORT=1234 -e APP_DB_HOST=server_mysql -e APP_DB_PORT=3300  -e APP_DB_USER=user -e APP_DB_PASSWORD=password -e APP_DB_NAME=database app:${env.BUILD_NUMBER}"

	  // -e APP_HOST=spring_docker_app   -e APP_PORT=8181 -e APP_DB_HOST=docker_spring_mysql -e APP_DB_PORT=3300  -e APP_DB_USER=user -e APP_DB_PASSWORD=password -e APP_DB_NAME=database

    }


}
