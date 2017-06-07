node("master") {
    try {
        stage('prepare') {
            git credentialsId: 'ddf4f338-b82c-487d-84ba-2e773825c02b', url: 'https://github.com/bkvin/qualite-laravel.git', branch: 'master'
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
            
                sshagent(['ddf4f338-b82c-487d-84ba-2e773825c02b']) {
                    sh('git push git@github.com:bkvin/qualite-laravel.git --all')
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
