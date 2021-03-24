
node {

   def registryProjet='registry.gitlab.com/thomas-lacheheb/jenkins-formation'
   def IMAGE="${registryProjet}:version-${env.BUILD_ID}"

    stage('Clone') {
          checkout scm
    }

    def img = stage('Build') {
          docker.build("$IMAGE",  '.')
    }

    stage('Run') {
          img.withRun("--name run-$BUILD_ID -p 9000:80") { c ->
                }
    }

    stage('Push') {
          docker.withRegistry('https://registry.gitlab.com', 'registry_id') {
              img.push 'latest'
              img.push()
          }
    }

}

