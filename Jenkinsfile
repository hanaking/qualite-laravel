node("master") {
    try {
        stage('prepare') {
            git credentialsId: 'f5df6f18-a8be-45f5-b484-71fb221cb629', url: 'https://github.com/bkvin/qualite-laravel.git', branch: 'master'
        }

        stage('build'){ 
            // sh "composer install"
        }

        stage('test') {
            // sh "./vendor/bin/phpunit"
        }

        stage('git'){  
            sh('git merge origin/dev')  
            sh('git commit -am "Merged develop branch to master')
            sh('git push origin master')
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
