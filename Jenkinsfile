@Library('gogox-agent-library') _

def test() {
  withCredentials([usernamePassword(credentialsId: "jenkins-service-account", passwordVariable: 'JIRA_TOKEN', usernameVariable: 'JIRA_EMAIL')]) {
    return "test 2"
  }
}


kuberneteAgent.call("ggvdevops/jenkins-test", "1.1", 60) {
  dir("build/${env.BUILD_ID}") {
    println test()
  }
}