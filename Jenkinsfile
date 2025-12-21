pipeline {
    agent any

    stages {

        stage('Clone Repository') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/sshaikh1005/nginx.git'
            }
        }

        stage('Install Nginx & Deploy Custom Page') {
            steps {
                sh '''
                    sudo apt-get update -y
                    sudo apt-get install nginx -y

                    sudo tee /var/www/html/index.html > /dev/null <<'EOF'
                    <html>
                        <head>
                            <title>Custom Nginx Page</title>
                        </head>
                        <body>
                            <h3>Welcome to my custom Nginx page served by Jenkins!</h3>
                            <h3>GitHub Webhook added...</h3>
                        </body>
                    </html>
                    EOF
                '''
            }
        }

        stage('Restart Nginx') {
            steps {
                sh 'sudo systemctl restart nginx'
            }
        }
    }
}
