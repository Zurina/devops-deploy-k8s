pipeline {
    agent any

    parameters {
        choice choices: ['qa', 'prod'], description: 'Select namespace for deployment', name: 'DEPLOY_TO'
    }

    environment{
        KUBE_CONFIG = credentials('kubeconfig')
    }

    stages {
        stage('Deploy Kubernetes') {
            steps {
                sh 'kubectl apply --kubeconfig $KUBE_CONFIG -f devops-app.yaml -n $DEPLOY_TO'
            }
        }
    }
}