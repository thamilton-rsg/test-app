node {

   stage('ARCHIVE') {
    git url: "https://github.com/thamilton-rsg/test-app.git"
    archiveArtifacts artifacts: '*', excludes: null, fingerprint: true
    sh "zip ${env.JOB_BASE_NAME}-${env.BUILD_NUMBER} *"
    // zip archive: true, dir: '', glob: '', zipFile: 'test.zip'
   }

   stage('ARTIFACTORY') {

   def uploadSpec = """
   {
      "files": [
        {
          "pattern": "${env.JOB_BASE_NAME}-${env.BUILD_NUMBER}.zip",
          "target": "test-app/${env.BRANCH_NAME}/"
        }
      ]
    }
   """

    // Get Artifactory server instance, defined in the Artifactory Plugin admin page.
    def server = Artifactory.server "ARTIFACTORY"

    // server username = "admin"
    // server password = "password"

    def buildUpload = server.upload spec: uploadSpec

    server.publishBuildInfo(buildUpload)

   }
}
