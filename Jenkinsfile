@Library('gogox-agent-library') _

import groovy.json.JsonSlurper

def parseDeployParams(params, deployParams) {
  if (params.countries) {
    deployParams.countries = Arrays.asList(params.countries.split(','))
  }

  deployParams.application = params.application ?: deployParams.application
  deployParams.notify_slack = params.notify_slack == null ? deployParams.notify_slack : params.notify_slack
  deployParams.envs = params.envs ?: deployParams.envs

  if (params.ticket_themes) {
    deployParams.ticket_themes = Arrays.asList(params.ticket_themes.split(','))
  }

  deployParams.transition_deployed_ticket_to_status = params.transition_deployed_ticket_to_status ?: deployParams.transition_deployed_ticket_to_status
  deployParams.cicd_image_name = params.cicd_image_name ?: deployParams.cicd_image_name

  if (params.env_namespace_mapping) {
    deployParams.env_namespace_mapping = stringToMap(params.env_namespace_mapping, deployParams.env_namespace_mapping)
  }

  if (params.env_cluster_mapping) {
    deployParams.env_cluster_mapping = stringToMap(params.env_cluster_mapping, deployParams.env_cluster_mapping)
  }

  if (params.env_app_tiller_namespace_mapping) {
    deployParams.env_app_tiller_namespace_mapping = stringToMap(params.env_app_tiller_namespace_mapping, deployParams.env_app_tiller_namespace_mapping)
  }

  if (params.env_cicd_sa_mapping) {
    deployParams.env_cicd_sa_mapping = stringToMap(params.env_cicd_sa_mapping, deployParams.env_cicd_sa_mapping)
  }

  deployParams.db_migraiton_cmd = params.db_migraiton_cmd ?: deployParams.db_migraiton_cmd

  if (params.extra_helm_value_files) {
    deployParams.extra_helm_value_files = Arrays.asList(params.extra_helm_value_files.split(','))
  }
}

def stringToMap(jsonString, defaultValue) {
  try {
    def map = [:]

    def jsonMap = new JsonSlurper().parseText(jsonString)
    jsonMap.each { key, value ->
      map[key] = value
    }
    return map
  } catch (Exception e) {
    println "Failed to parse jsonString [${jsonString}]. error: [${e}]"
    return defaultValue
  }
}

properties([
  parameters([
    string(name: 'countries', defaultValue: 'hk,sg'),
    string(name: 'application', defaultValue: 'gogovan-server-test'),
    booleanParam(name: 'notify_slack', defaultValue: false),
    string(name: 'envs', defaultValue: 'dev|qa'),
    string(name: 'ticket_themes', defaultValue: 'DET,BET'),
    string(name: 'transition_deployed_ticket_to_status', defaultValue: 'Ready for test'),
    string(name: 'cicd_image_name', defaultValue: 'gke-helm-v2-test'),
    string(name: 'env_namespace_mapping', defaultValue: '{"dev": "pf-dev", "stag": "pf-stag"}'),
    string(name: 'env_cluster_mapping', defaultValue: '{"prod": "k8scluster-prod-test", "default": "k8scluster-nonprod2-sg-test"}'),
    string(name: 'env_app_tiller_namespace_mapping', defaultValue: '{"default": "app-helm-tiller-test"}'),
    string(name: 'env_cicd_sa_mapping', defaultValue: '{"default": "ggv-sa-cicd-test"}'),
    string(name: 'db_migraiton_cmd', defaultValue: 'rails db:migrate'),
    string(name: 'extra_helm_value_files', defaultValue: 'shared_values.yaml,shared_values2.yaml')
  ])
])

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

parseDeployParams(params, deployParams)

// println deployParams

def test() {
  def agentLabel = "server-cd-dev-k8scluster-nonprod2-sg"
  def image = "gogotechhk/devops:gke-helm-v2"


  kuberneteAgent.deployAgent(agentLabel, image, "ggv-sa-cicd", "k8scluster-nonprod2-sg", ".*gogovan-server.*dev.*", 30, 1440) {
      stage('1') {
        println "test"
      }
  } { Exception e ->
    println e
  }
} 

test()