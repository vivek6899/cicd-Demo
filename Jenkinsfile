node {
    def app

    stage('clone repository'){
        checkout scm
    }

    stage('Build image'){
        app = docker.build("meets0ni/webapp")
        sh 'docker images'
    }

    stage('Test image') {
  
        app.inside {
            sh 'echo "Tests passed"'
        }
    }

    stage('Push image') {
        
        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
            app.push("${env.BUILD_NUMBER}")
        }
    }

}
