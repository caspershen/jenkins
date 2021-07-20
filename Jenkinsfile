

def test() {
  withCredentials([usernamePassword(credentialsId: "jenkins-service-account", passwordVariable: 'JIRA_TOKEN', usernameVariable: 'JIRA_EMAIL')]) {
    return sh(returnStdout: true, script: "echo 'test'")
  }
}

println test()
