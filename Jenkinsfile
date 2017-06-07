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
                // sh('git push --repo https://bkvin:sdftyui59@github.com/bkvin/qualite-laravel.git')
                withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: '9960d055-df1c-474a-ac3b-5bfdfbd4d59d', usernameVariable: 'GIT_USERNAME', passwordVariable: 'GIT_PASSWORD']]) {

                    sh('git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/bkvin/qualite-laravel.git')
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
