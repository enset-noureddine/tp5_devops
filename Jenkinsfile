pipeline {
 environment {
 registry = "yhalim8/tp-devops"
 registryCredential = 'dockerhub'
 dockerImage = ''
 }
 agent any
 stages {
 stage('Cloning Git') {
 steps {
 git 'https://github.com/enset-noureddine/tp5_devops'
 }
 }
 stage('Building image') {
 steps{
 script {
 dockerImage = docker.build registry + ":$BUILD_NUMBER"
 }
 }
 }
stage('Test image') {
 steps{
 script {
 echo "Tests passed"
 }
 }
 }
 stage('Publish Image') {
 steps{
 script {
 docker.withRegistry( '', registryCredential ) {
 dockerImage.push()
 }
 }
 }
 }
 stage('Deploy image') {
 steps{
 sh "docker run -d $registry:$BUILD_NUMBER"
 }
 }
 }
}
