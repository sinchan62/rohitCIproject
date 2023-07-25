pipeline {
    agent any
    tools {
        jdk "OracleJDK8"
        maven "MAVEN3"
    }
    environment {
        JAVA_HOME = '/usr/lib/jvm/java-1.8.0-openjdk-amd64'
        SNAP_REPO = 'vprofile-snapshot'
        NEXUS_USER = 'admin'
        NEXUS_PASS = 'admin123'
        RELEASE_REPO = 'vprofile-release'
        CENTRAL_REPO = 'vpro-maven-central'
        NEXUS_GRP_REPO = 'vpro-maven-group'
        NEXUXIP = '172.31.23.182'
        NEXUXPORT = '8081'
        NEXUS_LOGIN = 'nexuslogin'
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn -s settings.xml -DskipTests -e -X install'
            }
        }
    }
}
