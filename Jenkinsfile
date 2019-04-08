node {
  try {
    stage('Checkout') {
      checkout scm
    }
    stage('Environment') {
      sh 'git --version'
      echo "Branch: ${env.BRANCH_NAME}"
      sh 'printenv'
    }
    stage('Maven') {
      sh 'mvn clean '
      sh 'cp /opt/bitnami/apps/jenkins/jenkins_home/workspace/HelloWorld/dist/hello-world.war /home/bitnami/hello-world/'
    }
    stage('run test') {  
     sh 'mvn clean org.jacoco:jacoco-maven-plugin:prepare-agent test'
     sh ' mvn package sonar:sonar -Dsonar.host.url=http://35.154.234.38:9000'
    }
    stage('Docker_Build') {
      sh ' suod docker build -t mvn-app --no-cache .'
    }
    stage('Deploy') {
      sh ' docker run -d -p 8888:8888 mvn-app mvn-app'
    }
   }
  catch (err) {
    throw err
  }
}
