pipeline {
    agent any
    tools {
        jdk "OracleJDK8"
        maven "MAVEN3"
    }
    environment {
        JAVA_HOME = "${tool 'OracleJDK8'}"
        SNAP_REPO = 'vprofile-snapshot'
        NEXUS_USER = 'admin'
        NEXUS_PASS = 'admin123'
        RELEASE_REPO = 'vprofile-release'
        CENTRAL_REPO = 'vpro-maven-central'
        NEXUS_GRP_REPO = 'vpro-maven-group'
        NEXUXIP = ''
        NEXUXPORT = '8081'
        NEXUS_LOGIN = 'nexuslogin'
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn -s settings.xml -DskipTests install'
            }
        }
    }
}
