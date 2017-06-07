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
            // echo GIT_MERGE
            
            if (GIT_MERGE != "Already up-to-date.") {    
                // sh('git commit -am "Merged develop branch to master"')
                sh('git push https://alpha.aurigaeb@gmail.com:sdftyui59@https://github.com/bkvin/qualite-laravel.git --all')
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
