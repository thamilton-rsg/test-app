node {

   stage('ARCHIVE') {
     sh "ls -l"
     sh "pwd"
    step([$class: 'ArtifactArchiver', artifacts: '.', fingerprint: false])
   }

   stage('ARTIFACTORY') {

   def uploadSpec = """
    "files": [
      {
        "pattern": "*.zip",
        "target": "test-app/develop/"
      }
    ]
   """

    // Get Artifactory server instance, defined in the Artifactory Plugin admin page.
    def server = Artifactory.server "http://192.168.213.104:8081/artifactory"

    server username = "admin"
    server password = "password"

    def buildUpload = server.upload(uploadSpec)
    server.publishBuildInfo(buildUpload)

   }
}
