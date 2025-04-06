pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Modou255/my-app.git'
            }
        }
        stage('Tests') {
            steps {
                sh 'python -m pytest test_app.py -v'
            }
        }
        stage('Deploy with Ansible') {
            steps {
                ansiblePlaybook(
                    playbook: 'deploy.yml',
                    inventory: 'inventory.ini',
                    credentialsId: 'ansible-ssh-key'
                )
            }
        }
    }
    post {
        failure {
            emailext subject: 'Pipeline Failed',
                     body: 'Le pipeline a échoué. Vérifiez Jenkins.',
                     to: 'mamadoufall2023@gmail.com'
        }
    }
}
