pipeline{
    agent  any
    
    stages{
        stage('Git CheckOut'){
            steps{
                script{
                    git branch: 'main', url: 'https://github.com/palanivelgen/devops-practise.git'
                }
            }
        }
    }
}