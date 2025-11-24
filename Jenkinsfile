pipeline {
    agent any
    
    environment {
        DEPLOY_DIR = 'C:\\inetpub\\wwwroot\\2203116' // Create subfolder for your project
    }
    
    stages {
        stage('Checkout') {
            steps {
                echo 'Cloning project from GitHub...'
                git branch: 'main', url: 'https://github.com/mkaran02/RestaurantWebsite.git'
            }
        }
        
        stage('Build') {
            steps {
                echo 'Build Step: Check files in workspace'
                bat 'dir'
            }
        }
        
        stage('Deploy') {
            steps {
                echo 'Deploying all files to IIS folder'
                bat """
                    if not exist "${DEPLOY_DIR}" mkdir "${DEPLOY_DIR}"
                    xcopy /Y /E /I *.html "${DEPLOY_DIR}\\"
                    xcopy /Y /E /I *.css "${DEPLOY_DIR}\\"
                    xcopy /Y /E /I *.js "${DEPLOY_DIR}\\" 2>nul
                    echo Files deployed successfully
                    dir "${DEPLOY_DIR}"
                """
            }
        }
        
        stage('Run HTTP Server (Optional Test)') {
            steps {
                echo 'Skipping HTTP server (use IIS instead)'
            }
        }
    }
    
    post {
        success {
            echo 'Pipeline finished successfully! Visit:file:///C:/2203116/index.html'
        }
        failure {
            echo 'Pipeline failed! Check build logs.'
        }
    }
}
