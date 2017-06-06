node("master") {
    try {
        stage('prepare') {
            git credentialsId: 'f5df6f18-a8be-45f5-b484-71fb221cb629', url: 'https://github.com/bkvin/qualite-laravel.git', branch: 'master'
        }

        stage('build'){ 
            sh "cp .env.example .env"
            sh "composer install"
            sh "php artisan key:generate"
        }

        stage('test') {
            sh "./vendor/bin/phpunit"
        }

        stage('git'){  
            sh('git pull origin master')  
            sh('git merge origin dev')  
            sh('git commit -am "Merged develop branch to master')
            sh('git push origin master')
        }

        stage('cleanup') {
            // Recursively delete all files and folders in the workspace
            // using the built-in pipeline command
            deleteDir()
        }
    } catch(error) {
        throw error
    } finally {
    
    }
}
