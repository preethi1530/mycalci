node{
    stage('scm checkout'){
        git branch: 'main', credentialsId: 'gitcred', url: 'https://github.com/preethi1530/mycalci.git'
    }
        stage('execute maven'){
        def mvnHome = tool name: 'MAVEN_HOME', type: 'maven'
        def mvnCmd = "${mvnHome}/bin/mvn"
        sh "${mvnCmd} clean package"
    }
    stage('Build Docker image'){
        sh 'docker build -t preethib1530/calci:latest .'
    }
    stage('Push Docker image'){
        withCredentials([string(credentialsId: 'dockerhubpwd', variable: 'deockerhubp')]) {
    sh 'docker login -u preethib1530 --password ${deockerhubp}'
        }
        sh 'docker push preethib1530/calci:latest'
    }
  stage('run docker container on jenkins') {
         sh 'docker run -d -p 9090:8080 preethib1530/calci:latest'
    }
}
