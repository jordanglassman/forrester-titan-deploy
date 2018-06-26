node {
    properties([parameters([booleanParam(name: 'FAIL_BUILD', defaultValue: false, description: 'Force this build to FAILURE status')])])

    stage('checkout') {
        dir('module-a') {
            git url: 'https://github.com/jordanglassman/forrester-titan-backend.git'
        }
        dir('module-b') {
            git url: 'https://github.com/jordanglassman/forrester-titan-frontend.git'
        }
    }

    stage('build') {
        dir('module-a') {
            withMaven(maven: 'Maven350') {
                sh "mvn clean package"
            }
        }
        dir('module-b') {
            withMaven(maven: 'Maven350') {
                sh "mvn clean package"
            }
        }
    }

    if(params.FAIL_BUILD) {
        currentBuild.result = 'FAILURE'
        error('build failed due to UNSTABLE_BUILD param setting')
    }
}