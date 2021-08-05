@Library('test-lib') _

// properties([
//   parameters([
//     string(name: 'countries', defaultValue: 'hk,sg'),
//     string(name: 'application', defaultValue: 'gogovan-server-test'),
//     booleanParam(name: 'notify_slack', defaultValue: false),
//     string(name: 'envs', defaultValue: 'dev|qa'),
//     string(name: 'ticket_themes', defaultValue: 'DET,BET'),
//     string(name: 'transition_deployed_ticket_to_status', defaultValue: 'Ready for test'),
//     string(name: 'cicd_image_name', defaultValue: 'gke-helm-v2-test'),
//     string(name: 'env_namespace_mapping', defaultValue: '{"dev": "pf-dev", "stag": "pf-stag"}'),
//     string(name: 'env_cluster_mapping', defaultValue: '{"prod": "k8scluster-prod-test", "default": "k8scluster-nonprod2-sg-test"}'),
//     string(name: 'env_app_tiller_namespace_mapping', defaultValue: '{"default": "app-helm-tiller-test"}'),
//     string(name: 'env_cicd_sa_mapping', defaultValue: '{"default": "ggv-sa-cicd-test"}'),
//     string(name: 'db_migraiton_cmd', defaultValue: 'rails db:migrate'),
//     string(name: 'extra_helm_value_files', defaultValue: 'shared_values.yaml,shared_values2.yaml')
//   ]),
//   [$class: 'BuildBlockerProperty', blockLevel: 'Global',
//   blockingJobs: ".*gogovan-server.*dev.*", scanQueueFor: 'ALL',
//   useBuildBlocker: true],
//   disableConcurrentBuilds()
// ])

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

// deploy.parseDeployParams(params, deployParams)
deploy.call(deployParams)

// def test(deployParams) {
//   deploy.parseDeployParams(params, deployParams)
//   deploy.call(deployParams)
// }
// test(deployParams)

// def func1(Closure body) {
//   body.call()
// }

// def test(deployParams) {
//   println deployParams

//   println "A"
//   func1() {
//     println "B"
//     stage('(1) Initialization') {
//       println deployParams
//     }
//   }
// }

// test(deployParams)