pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
            }
            {
                sh "mvn clean package -DbuildNumber=${env.BUILD_NUMBER} -DskipTests=true"
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
            {
                cifsPublisher alwaysPublishFromMaster: false, continueOnError: false, failOnError: false, publishers: [[
                  configName: 'Automic', transfers: [[
                    cleanRemote: false, 
                    excludes: '', 
                    flatten: false, 
                    makeEmptyDirs: false, 
                    noDefaultExcludes: false, 
                    patternSeparator: '[, ]+', 
                    remoteDirectory: '', 
                    remoteDirectorySDF: false, 
                    removePrefix: 'target/', 
                    sourceFiles: 'target/*.jar']], 
                  usePromotionTimestamp: false, 
                  useWorkspaceInPromotion: false, 
                  verbose: true
                ]]
            }
            {
                createDepPckg appName: 'DIGITALBANK', folder: 'DEFAULT', owner: '100/AUTOMIC/AUTOMIC', pass: 'AUTOMIC', pkgName: '$BUILD_NUMBER', pkgType: 'Deployment', server: 'http://10.0.0.228:80/cda', useCentlCrd: true, user: '100/AUTOMIC/AUTOMIC'
            }
        }
    }
}
