pipeline {
    agent any

    parameters {
        choice choices: ['qa', 'prod'], description: 'Select namespace for deployment', name: 'DEPLOY_TO'
        string(name: 'IMAGE_ID', defaultValue: '', description: 'Docker IMAGE ID')
    }

    environment{
        KUBE_CONFIG = credentials('kubeconfig')
    }

    stages {
        stage('Deploy Kubernetes') {
            steps {
                sh "sed -i s/IMAGE_ID/${IMAGE_ID}/g devops-app.yaml"
                sh 'kubectl apply --kubeconfig $KUBE_CONFIG -f devops-app.yaml -n $DEPLOY_TO'
            }
        }
    }
}