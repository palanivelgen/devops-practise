@Library('common_shared_library') _
pipeline{
    agent  any
    tools {
        // Install the Maven version configured as "M3_HOME" and add it to the path.
        maven "M3_HOME"
    }

    parameters{
        choice(name: 'action',choices:'Create\nDestroy', description:'Choose Create/Destroy')
        string(name:'ImageName', description: 'Name of the docker build', defaultValue:'javaapp')
        string(name:'ImageTag', description: 'Name of the Image Tag', defaultValue:'v1')
        string(name:'DockerHubUserName', description: 'Name of the App', defaultValue:'pazhani11')    }

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

        stage('Quality Gate Status'){
        
        when{
            expression{params.action == 'Create'}
        }
            steps{
                script{

                    sleep(time:20,unit:"SECONDS")
                    timeout(time: 20,unit: 'SECONDS'){
                    def sonarQubeCredentials = 'sonarqube-api'
                    def qg=qualityGateStatus(sonarQubeCredentials)
                    print "Finished waiting"
                if (qg.status != 'OK') {
                     error "Pipeline aborted due to quality gate failure: ${qg.status}"
                        }   
                    }
                                    }
            }
        }

        stage('Maven Build : maven'){
        
        when{
            expression{params.action == 'Create'}
        }
            steps{
                script{
                   mvnBuild()
                }
            }
        }


 stage('Docker Image Build'){
        
        when{
            expression{params.action == 'Create'}
        }
        
        steps{
            script{
                dockerBuild("${params.ImageName}","${params.ImageTag}","${params.DockerHubUserName}")
            }
        }
        }

    stage('Docker Image Scan: Trivia'){    
        
        when{
            expression{params.action == 'Create'}
        }
        
        steps{
            script{
                dockerImageScan("${params.ImageName}","${params.ImageTag}","${params.DockerHubUserName}")
            }
        }
        }


    }
}
