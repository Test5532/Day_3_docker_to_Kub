
pipeline{
    agent{
        label "jenkins-agent"
    }

    environment {
        APP_NAME = "shopping-cart"

    }

    stages{
        stage("CLEANUP THE WORKSPACE")
        {
            steps{
                cleanWs()
            }
        }

        stage("GIT CHECKOUT FROM SCM")
        {
            steps{
                git branch: "main" , credentialsId: 'github' , url: 'https://github.com/Test5532/Day_3_docker_to_Kub'
            }
        }



        stage("Update Manifest file")
        {
            steps{
                sh """
                    cat deployment.yaml
                    sed -i 's/\${APP_NAME}.*/\${APP_NAME}:\${IMAGE_TAG}/g' deployment.yaml
                    cat deployment.yaml
                """
            }
        }

        stage("Push the changed deployment file to GIT")
        {
            steps{
                sh """
                    git config --global user.name "test5532"
                    git config --global user.email "karan.0requiem@gmail.com"
                    git add deployment.yaml
                    git commit -m "Updated Manifest with New Version"
                """
                withCredentials([gitUsernamePassword(credentialsId: 'github', gitToolName: 'Default')]) {
                    sh "git push https://github.com/Test5532/Day_3_docker_to_Kub main"
                }
            }          
        }
    }
}











