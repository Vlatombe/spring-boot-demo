pipeline {
    agent {
        kubernetes {
            label 'demo-spring-boot'
            yaml """
  spec:
    containers:
    - name: jnlp
    - name: jdk
      image: openjdk:8-jdk
      command:
      - cat
      tty: true
"""
        }
    }
    options {
        buildDiscarder(logRotator(numToKeepStr: '5'))
        disableConcurrentBuilds()
    }
    stages {
        stage('Build Java App') {
            steps {
                container('jdk') {
                    withMaven(mavenOpts: '-Dorg.slf4j.simpleLogger.log.org.apache.maven.cli.transfer.Slf4jMavenTransferListener=warn') {
                        sh './mvnw clean verify'
                    }
                }
            }
        }
    } // stages
}