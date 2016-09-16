node {

   stage('ARCHIVE') {
    sh "touch test.yml"
    sh "echo 'Hello world' >> test.yml"
    zip archive: true, dir: '', glob: '', zipFile: 'test.zip'
   }

   stage('ARTIFACTORY') {

   def uploadSpec = """
   {
      "files": [
        {
          "pattern": "*.zip",
          "target": "test-app/develop/"
        }
      ]
    }
   """

    // Get Artifactory server instance, defined in the Artifactory Plugin admin page.
    def server = Artifactory.server "ARTIFACTORY"

    // server username = "admin"
    // server password = "password"

    def buildUpload = server.upload(uploadSpec)

    server.publishBuildInfo(buildUpload)

   }
}
