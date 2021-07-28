@Library('gogox-agent-library') _

import groovy.json.JsonSlurper

def deployParams = [
  countries: ['hk', 'sg', 'tw', 'in', 'vn'],
  application:  'gogovan-server',
  notify_slack: true,
  envs: 'dev|qa|autoqa|stag|prod',
  ticket_themes: ['DET', 'BET', 'CET', 'PT', 'DT', 'IET'],
  transition_deployed_ticket_to_status: 'Ready for QA',
  cicd_image_name: 'gke-helm-v2',
  env_namespace_mapping: ["dev": "pf-dev", "stag": "pf-stag", "qa": "pf-qa", "autoqa": "pf-autoqa", "prod": "pf"],
  env_cluster_mapping: ["prod": "k8scluster-prod", "default": "k8scluster-nonprod2-sg"],
  env_app_tiller_namespace_mapping: ["default": "app-helm-tiller"],
  env_cicd_sa_mapping: ["default": "ggv-sa-cicd"],
  db_migraiton_cmd: "rails db:migrate",
  extra_helm_value_files: ['shared_values.yaml']
]

println new JsonSlurper().parseText('"dev": "pf-dev", "stag": "pf-stag"')

if (env.countries) {
  println "1"
  deployParams.countries = Arrays.asList(env.countries.split(','))
}

if (env.application) {
  deployParams.application = env.application
}

if (env.notify_slack) {
  println env.notify_slack
}

if (env.choice) {
  println env.choice
}

if (env.choice2) {
  println env.choice2
}

if (env.textparam) {
  println env.textparam
}


// println deployParams

// def test() {
//   withCredentials([usernamePassword(credentialsId: "jenkins-service-account", passwordVariable: 'JIRA_TOKEN', usernameVariable: 'JIRA_EMAIL')]) {
//     return "test 2"
//   }
// }


// kuberneteAgent.call("ggvdevops/jenkins-test", "1.1", 60) {
//   dir("build/${env.BUILD_ID}") {
//     println test()
//   }
// }