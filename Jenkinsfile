@Library('gogox-agent-library') _

import groovy.json.JsonBuilder
import groovy.json.JsonSlurper

// def params = [
//   countries: ['hk', 'sg', 'tw', 'in', 'vn'],
//   application:  'gogovan-server',
//   notify_slack: true,
//   envs: 'dev|qa|autoqa|stag|prod',
//   ticket_themes: ['DET', 'BET', 'CET', 'PT', 'DT', 'IET'],
//   transition_deployed_ticket_to_status: 'Ready for QA',
//   cicd_image_name: 'gke-helm-v2',
//   env_namespace_mapping: ["dev": "pf-dev", "stag": "pf-stag", "qa": "pf-qa", "autoqa": "pf-autoqa", "prod": "pf"],
//   env_cluster_mapping: ["prod": "k8scluster-prod", "default": "k8scluster-nonprod2-sg"],
//   env_app_tiller_namespace_mapping: ["default": "app-helm-tiller"],
//   env_cicd_sa_mapping: ["default": "ggv-sa-cicd"],
//   db_migraiton_cmd: "rails db:migrate",
//   extra_helm_value_files: ['shared_values.yaml']
// ]

// properties([
//   parameters([
//     string(
//       name: 'countries',
//       defaultValue: 'tw,hk',
//       description: 'countries'
//     )
//   ])
// )]

properties([
  parameters([
    string(name: 'countries', defaultValue: 'hk,sg,tw,in,vn'),
    string(name: 'application', defaultValue: 'gogovan-server'),
    booleanParam(name: 'notify_slack', defaultValue: true),
    string(name: 'ticket_themes', defaultValue: 'DET,BET,CET,PT,DT,IET'),
    string(name: 'transition_deployed_ticket_to_status', defaultValue: 'Ready for QA'),
    string(name: 'cicd_image_name', defaultValue: 'gke-helm-v2'),
    string(name: 'env_namespace_mapping', defaultValue: '{"dev": "pf-dev", "stag": "pf-stag", "qa": "pf-qa", "autoqa": "pf-autoqa", "prod": "pf"}'),
    string(name: 'env_cluster_mapping', defaultValue: '{"prod": "k8scluster-prod", "default": "k8scluster-nonprod2-sg"}'),
    string(name: 'env_app_tiller_namespace_mapping', defaultValue: '{"default": "app-helm-tiller"}'),
    string(name: 'env_cicd_sa_mapping', defaultValue: '{"default": "ggv-sa-cicd"}'),
    string(name: 'db_migraiton_cmd', defaultValue: 'rails db:migrate'),
    string(name: 'extra_helm_value_files', defaultValue: 'shared_values.yaml')
  ])
])

println params

def parseDeployParams(deployParams) {
  if (env.countries) {
    deployParams.countries = Arrays.asList(env.countries.split(','))
  }

  deployParams.application = env.application ?: deployParams.application
  deployParams.notify_slack = env.notify_slack ?: deployParams.notify_slack
  deployParams.envs = env.envs ?: deployParams.envs

  if (env.ticket_themes) {
    deployParams.ticket_themes = Arrays.asList(env.ticket_themes.split(','))
  }

  deployParams.transition_deployed_ticket_to_status = env.transition_deployed_ticket_to_status ?: deployParams.transition_deployed_ticket_to_status
  deployParams.cicd_image_name = env.cicd_image_name ?: deployParams.cicd_image_name

  if (env.env_namespace_mapping) {
    deployParams.env_namespace_mapping = stringToMap(env.env_namespace_mapping, deployParams.env_namespace_mapping)
  }

  if (env.env_cluster_mapping) {
    deployParams.env_cluster_mapping = stringToMap(env.env_cluster_mapping, deployParams.env_cluster_mapping)
  }

  if (env.env_app_tiller_namespace_mapping) {
    deployParams.env_app_tiller_namespace_mapping = stringToMap(env.env_app_tiller_namespace_mapping, deployParams.env_app_tiller_namespace_mapping)
  }

  if (env.env_cicd_sa_mapping) {
    deployParams.env_cicd_sa_mapping = stringToMap(env.env_cicd_sa_mapping, deployParams.env_cicd_sa_mapping)
  }

  deployParams.db_migraiton_cmd = env.db_migraiton_cmd ?: deployParams.db_migraiton_cmd

  if (env.extra_helm_value_files) {
    deployParams.extra_helm_value_files = Arrays.asList(env.extra_helm_value_files.split(','))
  }
}

def stringToMap(jsonString, defaultValue) {
  try {
    return new JsonSlurper().parseText(jsonString)
  } catch (Exception e) {
    println e
    return defaultValue
  }
}