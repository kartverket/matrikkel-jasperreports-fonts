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

    parameters {
        extendedChoice(
            name: 'version',
            description: 'Tagget versjon for publisering',
            value: "${listGitRefs(repo: GIT_URL, branches: false)}",
            defaultValue: '--',
            type: 'PT_SINGLE_SELECT',
            visibleItemCount: 10
        )
    }

    stages {
        stage('Validate') {
            steps {
                script {
                    if (params.version.startsWith('--')) {
                        currentBuild.result = 'ABORTED'
                        error('Du må velge versjon!')
                    }
                }
            }
        }

        stage('Publish') {
            steps {
                sh "./gradlew publish -Pversion=${params.version}"
            }
        }

    }

    post {
        success {
            deleteDir()
        }
        cleanup {
//            pushBuildFeed()
        }
    }
}
