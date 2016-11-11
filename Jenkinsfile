node {
    stage('SCM') {
        git 'https://github.com/wzhkun/Software-Project-Risk-Management-System'
    }
    stage('QA') {
    	sh 'export PATH = $PATH:/usr/local/sonar-scanner-2.8/bin'
        sh 'sonar-scanner'
    }
    stage('build') {
        def mvnHome = tool 'M3'
        sh "${mvnHome}/bin/mvn -B clean package"
    }
    stage('deploy') {
        sh "docker stop my || true"
        sh "docker rm my || true"
        sh "docker run --name my -p 11111:8080 -d tomcat"
        sh "docker cp target/SoftwareProjectRiskManagementSystem.war my:/usr/local/tomcat/webapps"
    }
    stage('results') {
        archiveArtifacts artifacts: '**/target/*.war', fingerprint: true
    }
}
