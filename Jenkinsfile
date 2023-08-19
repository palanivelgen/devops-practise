@Library('common_shared_library') _
pipeline{
    agent  any
    tools {
        // Install the Maven version configured as "M3_HOME" and add it to the path.
        maven "M3_HOME"
    }

    parameters{
        choice(name: 'action',choices:'Create\nDestroy', description:'Choose Create/Destroy')
    }

    stages{

        
        stage('Git CheckOut'){
        
        when{
            expression{params.action == 'Create'}
        }

            steps{
                
                    gitCheckout(
                        branch:"main",
                        url: "https://github.com/palanivelgen/devops-practise.git"
                    )
                
            }
        }
        stage('Maven Test'){
        
        when{
            expression{params.action == 'Create'}
        }
        
        steps{
            script{
                mvnTest()
            }
        }
        }

        stage('Maven Integration Test'){
        
        when{
            expression{params.action == 'Create'}
        }
            steps{
                script{
                    mvnIntegrationTest()
                }
            }
        }

        stage('Static Code Analysis'){
        
        when{
            expression{params.action == 'Create'}
        }
            steps{
                script{
                    def sonarQubeCredentials = 'sonarqube-api'

                    staticCodeAnalysis(sonarQubeCredentials)
                }
            }
        }
        
    }
}
