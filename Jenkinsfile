pipeline {
    agent any
    
    environment {
        SEMGREP_APP_TOKEN = credentials('Semgrep')
    }
    
    stages {
        stage('Semgrep-Scan') {
            steps {
                script {
                    // Pull the Semgrep Docker image
                    docker.image('returntocorp/semgrep').pull()
                    
                    // Run Semgrep scan
                    docker.image('returntocorp/semgrep').run(
                        "-e SEMGREP_APP_TOKEN=${env.SEMGREP_APP_TOKEN}",
                        "-v ${pwd()}:${pwd()} --workdir ${pwd()}",
                        'returntocorp/semgrep',
                        'semgrep ci'
                    )
                }
            }
        }
    }
}
