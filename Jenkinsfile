node {
  try {
    stage('Checkout') {
      checkout scm
    }
    stage('Environment') {
      echo "$USER"
      sh 'git --version'
      echo "Branch: ${env.BRANCH_NAME}"
      sh 'printenv'
    }
    stage('Maven') {
      sh 'mvn clean '
      sh 'cp /var/lib/jenkins/workspace/HelloWorld/dist/hello-world.war /var/lib/jenkins/workspace/HelloWorld/'
    }
    stage('Docker_Build') {
      sh ' sudo docker build -t mvn-app --no-cache .'
    }
    stage('Deploy') {
      sh 'sudo docker run -d -p 8080:8080 --name mvn-app mvn-app'
    }
   }
  catch (err) {
    throw err
  }
}
