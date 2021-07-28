@Library('gogox-agent-library') _

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

println COUNTRIES
println countries
if (env.COUNTRIES) {
  println "1"
  deployParams.countries = Arrays.asList(COUNTRIES.split(','))
}

if (binding.hasVariable('countries')) {
  println "2"
  deployParams.countries = Arrays.asList(countries.split(','))
}

if (binding.hasVariable('APPLICATION')) {
  deployParams.application = APPLICATION
}

if (binding.hasVariable('NOTIFY_SLACK')) {
  println NOTIFY_SLACK
}

if (binding.hasVariable('CHOICE')) {
  println CHOICE
}

if (binding.hasVariable('CHOICE2')) {
  println CHOICE2
}

if (binding.hasVariable('TEXTPARAM')) {
  println CHOICE2
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