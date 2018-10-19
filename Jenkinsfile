pipeline {
    agent none
    options {
        buildDiscarder(logRotator(numToKeepStr: '5'))
        disableConcurrentBuilds()
    }
    stages {
        stage('Build java app') {
            parallel {
                stage('Debian') {
                    agent {
                        kubernetes {
                            label 'demo-spring-boot-debian'
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
                        } // kubernetes
                    } // agent
                    steps {
                        container('jdk') {
                                sh './mvnw clean verify'
                        }
                    } // steps
                } // stage
                stage('Alpine') {
                    agent {
                        kubernetes {
                            label 'demo-spring-boot-alpine'
                            yaml """
                spec:
                    containers:
                    - name: jnlp
                    - name: jdk
                    image: openjdk:8-jdk-alpine
                    command:
                    - cat
                    tty: true
                """
                        } // kubernetes
                    } // agent
                    steps {
                        container('jdk') {
                            sh './mvnw clean verify'
                        }
                    } // steps
                } // stage
                stage('CentOS') {
                    agent {
                        kubernetes {
                            label 'demo-spring-boot-centos'
                            yaml """
                spec:
                    containers:
                    - name: jnlp
                    - name: jdk
                    image: fabric8/java-centos-openjdk8-jdk
                    command:
                    - cat
                    tty: true
                """
                        } // kubernetes
                    } // agent
                    steps {
                        container('jdk') {
                            sh './mvnw clean verify'
                        }
                    } // steps
                } // stage
            } // parallel
        } // stage
    } // stages
}
