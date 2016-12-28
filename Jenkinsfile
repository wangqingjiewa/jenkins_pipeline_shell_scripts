node {
   
   	stage 'Checkout'
   		git url: 'https@github.com:wangqingjiewa/jenkins_pipeline_shell_scripts.git'
   	stage 'Build'
   		sh './myBuild.sh'
    stage "testing"
      echo '执行 JMeter 测试'
      sh "curl -uadmin:password -X GET 'http://localhost:9080/jenkins/job/Mvn-Jmeter/artifactory/staging?releaseVersion=1.1&nextVersion=1.2-SNAPSHOT&createReleaseBranch=false&createVcsTag=true&tagUrl=1.1&tagComment=1.1&nextDevelCommitComment='"
    

    stage 'Promotion'

    git url: 'https://github.com/jfrogdev/project-examples.git'

    // Get Artifactory server instance, defined in the Artifactory Plugin administration page.
    def server = Artifactory.server 'docker@local'

    // Create the upload spec.
    def uploadSpec = readFile 'jenkins-pipeline-examples/resources/props-upload.json'

    // Upload to Artifactory.
    def buildInfo = server.upload spec: uploadSpec

    // Create the download spec.
    def downloadSpec = readFile 'jenkins-pipeline-examples/resources/props-download.json'

    // Download from Artifactory.
    server.download spec: downloadSpec, buildInfo: buildInfo

    // Publish the build to Artifactory
    server.publishBuildInfo buildInfo
    
    def promotionConfig = [
        //Mandatory parameters
        'buildName'          : buildInfo.name,
        'buildNumber'        : buildInfo.number,
        'targetRepo'         : 'libs-release-local',

        //Optional parameters
        'comment'            : 'This build has been tested and was ready to promote',
        'sourceRepo'         : 'libs-snapshot-local',
        'status'             : 'Released',
        'includeDependencies': true,
        'copy'               : true
    ]

    // Promote build
    server.promote promotionConfig
   
   stage 'Deploy'
         git url: 'https@github.com:wangqingjiewa/jenkins_pipeline_shell_scripts.git'
   		sh './myDeployment.sh'
  
}
