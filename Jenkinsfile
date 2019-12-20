pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
            }
            {
                sh "mvn clean package -DskipTests=true"
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
                    sourceFiles: 'target/*.jar', 
                  usePromotionTimestamp: false, 
                  useWorkspaceInPromotion: false, 
                  verbose: true
                ]]
            }
        }
    }
}
