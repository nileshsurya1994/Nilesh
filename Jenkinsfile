pipeline {
    agent any

    tools {
        nodejs14 "nodejs"
    }

    stages {
        // Your existing stages here...

        stage('Deploy') {
            environment {
                DEPLOY_SSH_KEY = credentials('AWS_INSTANCE_SSH')
                PRODUCTION_IP_ADDRESS = 'YOUR_PRODUCTION_IP_ADDRESS'
            }

            steps {
                sh """
                    ssh -v -i ${DEPLOY_SSH_KEY} ubuntu@${PRODUCTION_IP_ADDRESS} '
                        if [ ! -d "todos-app" ]; then
                            git clone https://github.com/nileshsurya1994/Nilesh.git 
                            cd todos-app
                        else
                            cd todos-app
                            git pull
                        fi

                        yarn install

                        if pm2 describe todos-app > /dev/null ; then
                            pm2 restart todos-app
                        else
                            yarn start:pm2
                        fi
                    '
                """
            }
        }
    }
}
