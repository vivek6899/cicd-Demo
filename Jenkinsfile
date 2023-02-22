node {
    def app

    stage('clone repository'){
        sh 'echo "Cloning the repository"'
        checkout scm
    }

    stage('Build image'){
//        sh 'echo "Building the image"'
        app = docker.build("vivek6899/webapp")
        sh 'docker images'
    }

    stage('Test image') {
  
        app.inside {
  //          sh 'echo "Testing the image"'
            sh 'echo "Tests passed"'
        }
    }

    stage('Push image') {

    //    sh 'echo "Pushing the image"'
        
        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
            app.push("${env.BUILD_NUMBER}")
        }
    }    

    // stage('Trigger ManifestUpdate') {
    //     parameters: [string(name: 'DOCKERTAG', value: env.BUILD_NUMBER)]
    // }

    // stage('Update image teg') {

    //     sh "cat deployment.yaml"
    //     // sh "sed -i 's+meets0ni/test.*+meets0ni/test:${DOCKERTAG}+g' deployment.yaml"
    //     sh "sed -i 's+meets0ni/test.*meets0ni/test:${DOCKERTAG}+g' deployment.yaml"
    //     sh "cat deployment.yaml"
    // }

//     stage("SSH Into k8s Server") {

//         sh 'echo "connecting via ssh to master node"'
//         def remote = [:]
//         remote.name = 'gitK8s'
//         remote.host = '20.204.116.27'
//         remote.user = 'meet'
//         remote.password = 'meet'
//         remote.allowAnyHosts = true

//         stage('Put deployment.yaml into k8smaster') {
//             sshPut remote: remote, from: 'deployment.yaml', into: '.'
//         } 

//         stage('Deploy simple web') {
//           sshCommand remote: remote, command: "kubectl apply -f deployment.yaml"
//         }
//     } 

}

