pipeline {
    agent any
    
    stages {
        stage('Clone') {
            steps {
                script {
                    git clone "https://github.com/sshaikh1005/nginx.git"
                }
            }
        }
        stage('Custom Page to Nginx') {
            steps {
                script {
                    sh 'sudo apt update'
                    sh 'sudo apt install nginx -y'
                    def htmlContent = """
                    <html>
                        <head>
                            <title>Custom Nginx Page</title>
                        </head>
                        <body>
                            <h1>Welcome to my custom Nginx page served by Jenkins!</h1>
                            <h3>Github Webhook added...</h3>
                        </body>
                    </html>
                    """
                    sh """
                    echo '${htmlContent}' | sudo tee /var/www/html/index.html
                    """
                }
            }
        }
        stage('Restart Nginx') {
            steps {
                script {
                    sh 'sudo systemctl restart nginx'
                }
            }
        }
    }
}
