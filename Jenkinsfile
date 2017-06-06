node("docker") {
    docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
    
        git url: "https://github.com/bkvin/qualite-laravel.git", credentialsId: '537f87ec-2069-4c2b-b75d-a5d916bc8393'
    
        sh "git rev-parse HEAD > .git/commit-id"
        def commit_id = readFile('.git/commit-id').trim()
        println commit_id
    
        stage "build"
        def app = docker.build "your-project-name"
    
        stage "publish"
        app.push 'master'
        app.push "${commit_id}"
    }
}
