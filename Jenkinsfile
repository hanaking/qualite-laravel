node("master") {
    try {
        stage('prepare') {
            git credentialsId: 'f5df6f18-a8be-45f5-b484-71fb221cb629', url: 'https://github.com/bkvin/qualite-laravel.git', branch: 'master'
            sh('git config --global user.email "alpha.aurigaeb@gmail.com"')
            sh('git config --global user.name "bkvin"')
        }

        stage('build'){ 
            // sh "composer install"
        }

        stage('test') {
            // sh "./vendor/bin/phpunit"
        }

        stage('git'){  
            
            GIT_MERGE = sh(returnStdout: true, script: 'git merge origin/dev').trim()
            
            if (GIT_MERGE != "Already up-to-date.") { 
                withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'f5df6f18-a8be-45f5-b484-71fb221cb629', usernameVariable: 'GIT_USERNAME', passwordVariable: 'GIT_PASSWORD']]) {

                    sh('git push https://${GIT_USERNAME}:${GIT_PASSWORD}@<REPO>')
                }   
            }            
        }
    } catch(error) {
        throw error
    } finally {
    
        stage('cleanup') {
            // Recursively delete all files and folders in the workspace
            // using the built-in pipeline command
            deleteDir()
        }
    }
}
