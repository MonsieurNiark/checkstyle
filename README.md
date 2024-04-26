pipeline {
 agent any
 stages {
 stage('Checkout') {
 steps {
 // Cloner le code depuis GitHub
 git branch: 'master', credentialsId: 'mot de passe github', url:
'https://github.com/votre_username/checkstyle'
 }
 }
 stage('Build') {
 parallel {
 stage('Maven build') {
 steps {
 sh "mvn clean install"
 }
 }
 stage('Checkstyle') {
 steps {
 sh "mvn checkstyle:check"
 recordIssues(tools: [checkStyle(reportEncoding: 'UTF-8')])
 }
 }
 }
 }
 }
}
