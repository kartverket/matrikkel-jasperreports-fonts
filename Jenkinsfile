@Library('common') _

pipeline {
    agent any

    tools {
        jdk 'Java 11 Latest'
    }

    environment {
        // URI for repository som det skal deployes til
        // Denne må være på formen http(s)://<brukernavn>:<passord>@<repository>
        MAVEN_PUBLISH = credentials('MAVEN_DEPLOY_RELEASES')
    }


    options {
        timestamps()
        buildDiscarder(logRotator(numToKeepStr: '30'))
        disableConcurrentBuilds()

        // Ikke publish hvis bygget er ustabilt
        skipStagesAfterUnstable()
    }


    stages {
        stage('Validate') {
            steps {
                script {
                    if ("${TAG_NAME}" == "") {
                        currentBuild.result = 'ABORTED'
                        error('Må bygges med tagget version!')
                    }
                }
            }
        }

        stage('Publish') {
            when {
                allOf {
                    buildingTag()
                }
            }
            steps {
                sh "./gradlew publish -Pversion=${TAG_NAME}"
            }
        }

    }

    post {
        success {
            deleteDir()
        }
        cleanup {
            pushBuildFeed()
        }
    }
}
