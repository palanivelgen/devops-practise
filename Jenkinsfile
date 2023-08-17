@library(common_shared_library) _
pipeline{
    agent  any
    
    stages{
        stage('Git CheckOut'){
            steps{
                script{
                    gitCheckout(
                        branch:"main"
                        url: "https://github.com/palanivelgen/devops-practise.git"
                    )
                }
            }
        }
    }
}