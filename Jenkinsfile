node("master") {
    try {
        stage('prepare') {
            git credentialsId: '4dec68b7-2d02-4443-beb7-ac21b4a54a14', url: 'https://github.com/bkvin/qualite-laravel.git', branch: 'master'
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
            
                sshagent(['4dec68b7-2d02-4443-beb7-ac21b4a54a14']) {
                    sh('git push ssh://github.com:22/bkvin/qualite-laravel.git --all')
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
