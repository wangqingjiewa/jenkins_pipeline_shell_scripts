node {
   
   	stage 'Stage 1'
   		echo 'Hello there, shell scripts'
   	stage 'Checkout'
   		git url: 'https://github.com/TTFHW/jenkins_pipeline_shell_scripts.git'
   	stage 'Build'
   		sh './myBuild.sh'
      stage "testing"
      echo '执行 JMeter 测试'
      sh "curl -uadmin:password -X GET 'http://localhost:9080/jenkins/job/Mvn-Jmeter/artifactory/staging?releaseVersion=1.1&nextVersion=1.2-SNAPSHOT&createReleaseBranch=false&createVcsTag=true&tagUrl=1.1&tagComment=1.1&nextDevelCommitComment='"

   	stage 'Deploy'
   		sh './myDeployment.sh'
  
}
