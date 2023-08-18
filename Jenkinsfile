@Library('common_shared_library') _
pipeline{
    agent  any
    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "M3_HOME"
    }
    stages{
        stage('Git CheckOut'){
            steps{
                
                    gitCheckout(
                        branch:"main",
                        url: "https://github.com/palanivelgen/devops-practise.git"
                    )
                
            }
        }
        stage('Maven Test'){
        steps{
            script{
                mvnTest()
            }
        }
        }

        stage('Maven Integration Test'){
            steps{
                script{
                    mvnIntegrationTest()
                }
            }
        }
    }
}
