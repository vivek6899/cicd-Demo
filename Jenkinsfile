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

    stage("SSH Into k8s Server") {
        def remote = [:]
        remote.name = 'k8smaster'
        remote.host = '13.233.54.174'
        remote.user = 'meet'
        remote.password = 'meet'
        remote.allowAnyHosts = true

}

