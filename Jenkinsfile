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
                    withMaven(globalMavenSettingsConfig: 'repo.core.latombe.fr') {
                        sh './mvnw clean verify'
                    }
                }
            }
        }
    } // stages
}
