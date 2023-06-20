pipeline {
    agent any

    stages {
        stage('Input') {
            steps {
                input('Do you want to proceed?')
            }
        }

        stage('If Proceed is clicked') {
            steps {
                print('hello')
            }
        }
    }
}

pipeline {
  agent any
  tools {
        git 'Default'
        terraform 'Terraform'
        }
  stages {
    stage('SCM') {
        steps {
            cleanWS()
            git 'https://github.com/darkn3rd/webmf-python-flask.git'
            sh 'git clone https://github.com/darkn3rd/webmf-python-flask.git'
        }
    }
    stage('build') {
        steps {
            sh 'pip install -r requirements.txt'
      }
    }
    stage('test') {
        steps {
            sh 'python test.py'
        }
      post {
        always {
          junit 'test-reports/*.xml'
        }
      }    
    }
  }
}

pipeline {
  environment {
    // environment variables and credential retrieval can be interspersed
    SOME_VAR = "SOME VALUE"
    // this assumes that "cred1" has been created on Jenkins Credentials
    CRED1 = credentials("DockerHub")
    INBETWEEN = "Something in between"
    // this assumes that "cred2" has been created in Jenkins Credentials
    CRED2 = credentials("qwerty")
    // Env variables can refer to other variables as well
    OTHER_VAR = "${SOME_VAR}"
  }

  agent any

  stages {
    stage("foo") {
      steps {
        // environment variables are not masked
        sh 'echo "SOME_VAR is $SOME_VAR"'
        sh 'echo "INBETWEEN is $INBETWEEN"'
        sh 'echo "OTHER_VAR is $OTHER_VAR"'

        // credential variables will be masked in console log but not in archived file
        sh 'echo $CRED1 > cred1.txt'
        sh 'echo $CRED2 > cred2.txt'
        archive "**/*.txt"
      }
    }
}
}

pipeline {
    agent any
    stages {
        stage('Example') {
            input {
                message "Let's promote?"
                ok 'Release!'
                parameters {
                    extendedChoice defaultValue: 'blue,green,yellow,blue', description: '', descriptionPropertyValue: 'blue,green,yellow,blue', multiSelectDelimiter: ',', name: 'favColor', quoteValue: false, saveJSONParameterToFile: false, type: 'PT_MULTI_SELECT', value: 'blue,green,yellow,blue', visibleItemCount: 5
                }
            }
            steps {
                echo "Your favorite color is ${favColor}"
            }
            
        }
        stage('Mine'){
            input {
                message 'lets go'
                ok 'Yes'
                parameters {
                extendedChoice description: 'select', multiSelectDelimiter: ',', name: 'color', quoteValue: false, saveJSONParameterToFile: false, type: 'PT_MULTI_SELECT', value: '1,2,3', visibleItemCount: 5
                }
            }
            steps {
                echo "your favorite choice is ${color}"
            }
        }
    }
}

pipeline{
    agent any
    tools {
        git 'Default'
    }
    stages{
        stage('Stage 1'){
            steps{
                cleanWs()
                sh 'echo Connecting Private Remote Repository'
                git branch: 'main', credentialsId: 'GJJS', url: 'https://github.com/yagnasivasai/maven-private.git'
                sh 'git clone https://yagnasivasai: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@github.com/yagnasivasai/maven-private.git'
            }
        }
        stage('Stage 2'){
            steps{
                sh 'echo testing python code'
            }
        }
        stage('Stage 3'){
            steps{
                sh 'echo Deployingto staging'
            }
        }
        stage('Stage 4'){
            input {
                message 'Can we Proceed to Production?'
                ok 'Yes'
            }
            steps{
                sh 'echo Deploying to Production'
                sh 'git pull https://yagnasivasai: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@github.com/yagnasivasai/maven-private.git'
            }
        }
    }
    
}



pipeline {
  agent any
  parameters {
    choice(
      name: 'Env',
      choices: ['DEV', 'QA', 'UAT', 'PROD'],
      description: 'Passing the Environment'
    )
  }
  stages {
    stage('Environment') {
      steps {
        echo " The environment is ${params.Env}"
      }
    }
  }
}

pipeline {
    agent any

    stages {
        stage('Input') {
            steps {
                input('Do you want to proceed?')
            }
        }

        stage('Wait for user to input text?') {
            steps {
                script {
                    def userInput = input(id: 'userInput', message: 'Merge to?',
                    parameters: [[$class: 'ChoiceParameterDefinition', defaultValue: 'strDef', 
                        description:'describing choices', name:'nameChoice', choices: "QA\nUAT\nProduction\nDevelop\nMaster"]
                    ])

                    println(userInput); //Use this value to branch to different logic if needed
                }
            }
        }
        stage('If Proceed is clicked') {
            steps {
                print('hello')
            }
        }
    }
}


pipeline {
    agent any

    stages {
        stage('Input') {
            steps {
                input('Do you want to proceed?')
            }
        }

        stage('Wait for user to input text?') {
            steps {
                script {
                    def userInput = input(id: 'userInput', message: 'Merge to?',
                    parameters: [[$class: 'ChoiceParameterDefinition', defaultValue: 'strDef', 
                        description:'describing choices', name:'nameChoice', choices: "QA\nUAT\nProduction\nDevelop\nMaster"]
                    ])

                    println(userInput); //Use this value to branch to different logic if needed
                }
            }
        }
        stage('Other script'){
            steps{
                script {
            // Define Variable
                def USER_INPUT = input(
                    message: 'User input required - Some Yes or No question?',
                    parameters: [
                            [$class: 'ChoiceParameterDefinition',
                             choices: ['no','yes'].join('\n'),
                             name: 'input',
                             description: 'Menu - select box option']
                    ])

            echo "The answer is: ${USER_INPUT}"

            if( "${USER_INPUT}" == "yes"){
                //do something
            } else {
                //do something else
            }
        }
            }
            
        }
        stage('If Proceed is clicked') {
            steps {
                print('hello')
            }
        }
    }
}





// pipeline 
// { 
//     agent any
//     parameters
//     { 
//         gitParameter branchFilter: 'origin/(.*)', defaultValue: 'master', name: 'BRANCH', type: 'PT_BRANCH' 
//     }
//     stages 
//     { 
//        stage("list all branches") 
//        { 
//            steps 
//            { 
//                 git branch: "${params.BRANCH}", credentialsId: "SSH_user_name_with_private_key", url: "ssh://git@myCompanyBitBucketSite.com:port/myRepository.git" 
//            } 
//       } 
//    } 
// }


pipeline 
{ 
    agent any
    parameters
    { 
        gitParameter branchFilter: 'origin/(.*)', defaultValue: 'master', name: 'BRANCH', type: 'PT_BRANCH' 
    }
    stages 
    { 
       stage("list all branches") 
       { 
           steps 
           { 
                git branch: "${params.BRANCH}",'https://github.com/yagnasivasai/k8s-tutorial-python.git'
           } 
      } 
   } 
}

git branch:BRANCH[7..-1], url: 'https://github.com/yagnasivasai/k8s-tutorial-python.git'

pipeline 
{ 
    agent any 
    parameters {
    choice choices: ['master', 'dependabot/pip/django-poll-project/django-2.2.13', 'development'], description: 'Select the Branch', name: 'Git'
    }
    stages 
    { 
       stage("list all branches") 
       { 
           steps 
           { 
                git branch: "${params.Git}", 'https://github.com/yagnasivasai/k8s-tutorial-python.git' 
           } 
      } 
   } 
}


pipeline {
    agent  { label 'OPENJDK-11-MAVEN' }
    parameters {
        choice(name: 'BRANCH_TO_BUILD', choices: ['REL_INT_1.0', 'main'], description: 'Branch to build')
        string(name: 'MAVEN_GOAL', defaultValue: 'package', description: 'maven goal')

    }
    stages {
        stage('vcs') {
            steps {
                git branch: "${params.BRANCH_TO_BUILD}", url: 'https://github.com/GitPracticeRepo/spring-petclinic.git'
            }

        }
        stage('build') {
            steps {
                sh "/opt/apache-maven-3.8.6/bin/mvn ${params.MAVEN_GOAL}"
            }
        }
        stage('archive results') {
	

pipeline {
    agent any
    
    stages {
         
        stage("Interactive_Input") {
            steps {
                script {
                def userInput = input(
                 id: 'userInput', message: 'Enter path of test reports:?', 
                 parameters: [
                 [$class: 'TextParameterDefinition', defaultValue: 'None', description: 'Path of config file', name: 'Config'],
                 [$class: 'TextParameterDefinition', defaultValue: 'None', description: 'Test Info file', name: 'Test']
                ])
                echo ("IQA Sheet Path: "+userInput['Config'])
                echo ("Test Info file path: "+userInput['Test'])
                              
                }
            }
        }
    }
}

pipeline {

    agent any

    stages {

        stage("Interactive_Input") {
            steps {
                script {

                    // Variables for input
                    def inputConfig
                    def inputTest

                    // Get the input
                    def userInput = input(
                            id: 'userInput', message: 'Enter path of test reports:?',
                            parameters: [

                                    string(defaultValue: 'None',
                                            description: 'Path of config file',
                                            name: 'Config'),
                                    string(defaultValue: 'None',
                                            description: 'Test Info file',
                                            name: 'Test'),
                            ])

                    // Save to variables. Default to empty string if not found.
                    inputConfig = userInput.Config?:''
                    inputTest = userInput.Test?:''

                    // Echo to console
                    echo("IQA Sheet Path: ${inputConfig}")
                    echo("Test Info file path: ${inputTest}")

                    // Write to file
                    writeFile file: "inputData.txt", text: "Config=${inputConfig}\r\nTest=${inputTest}"

                    // Archive the file (or whatever you want to do with it)
                    archiveArtifacts 'inputData.txt'
                }
            }
        }
    }
}



pipeline{
    agent any
    tools {
        git 'Default'
    }
    stages{
        stage('Stage 1'){
            steps{
                cleanWs()
                sh 'echo Connecting Private Remote Repository'
                git branch: 'main', credentialsId: 'GJJS', url: 'https://github.com/yagnasivasai/maven-private.git'
                sh 'git clone https://yagnasivasai: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@github.com/yagnasivasai/maven-private.git'
            }
        }
        stage('Stage 2'){
            steps{
                sh 'echo testing python code'
            }
        }
        stage('Stage 3'){
            steps{
                sh 'echo Deploying to staging'
            }
        }
        stage('Stage 4'){
            input {
                message 'Can we Proceed to Production?'
                ok 'Yes'
            }
            steps{
                sh 'ssh -o StrictHostKeyChecking=no username@192.168.0.1 "source venv/bin/activate; \
                cd polling; \
                git pull https://yagnasivasai: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@github.com/yagnasivasai/maven-private.git; \
                echo Deploying to Production; \
                pip install -r requirements.txt --no-warn-script-location; \
                python manage.py makemigrations; \
                python manage.py migrate; \
                python manage.py collectstatic; \
                deactivate; \
                sudo systemctl restart gunicorn; \
                sudo systemctl restart nginx" '
            }
        }
    }
    
}

pipeline {
    agent any
    tools {
        git 'Default'
        terraform 'terraform'
    }

    stages {
        stage('Checkout SCM') {
            steps {
                cleanWs()
                git branch: 'terraform-jenkins-pipeline', credentialsId: 'Github', url: 'https://github.com/yagnasivasai/terraform.git'
                sh 'git clone https://github.com/yagnasivasai/terraform.git'
            }
        }

        stage('Building Docker Image'){
            steps{
                sh '''
                    cd task_8_terraform_integration
                    echo "alias docker='sudo docker'" >> ~/.bashrc
                    sudo usermod -aG docker $USER
                    sudo chmod 777 /var/run/docker.sock
                    docker build -t yaznasivasai/web:v1 .
                '''
            }
        }

        stage('Pushing Docker Images to DockerHub'){
            steps{
                withCredentials([string(credentialsId: 'DockerHub', variable: 'DockerPasswd')]) {
                sh "docker login -u yaznasivasai -p ${DockerPasswd}"
            }
                sh 'docker push yaznasivasai/web:v1'
            }
            
        }

        stage('Resource Creation') {
            steps {
                 sh '''
                    echo $BUILD_NUMBER
                    cd task_8_terraform_integration
                    terraform init
                    terraform plan
                    terraform apply -auto-approve
                    terraform show
                '''
            }
        }
    }
}




pipeline {
    agent any
    tools {
        git 'Default'
        terraform 'terraform'
    }

    stages {
        stage('Checkout SCM') {
            steps {
                cleanWs()
                git branch: 'terraform-jenkins-pipeline', credentialsId: 'Github', url: 'https://github.com/yagnasivasai/terraform.git'
                sh 'git clone https://github.com/yagnasivasai/terraform.git'
            }
        }

        stage('Building Docker Image'){
            steps{
                sh '''
                    cd task_8_terraform_integration
                    echo "alias docker='sudo docker'" >> ~/.bashrc
                    sudo usermod -aG docker $USER
                    sudo chmod 777 /var/run/docker.sock
                    docker build -t yaznasivasai/web:v1 .
                '''
            }
        }

        stage('Pushing Docker Images to DockerHub'){
            steps{
                withCredentials([string(credentialsId: 'DockerHub', variable: 'DockerPasswd')]) {
                sh "docker login -u yaznasivasai -p ${DockerPasswd}"
            }
                sh 'docker push yaznasivasai/web:v1'
            }
            
        }

        // stage('Resource Creation') {
        //     steps {
        //          sh '''
        //             echo $BUILD_NUMBER
        //             cd task_8_terraform_integration
        //             terraform init
        //             terraform plan
        //             terraform apply -auto-approve
        //             terraform show
        //         '''
        //     }
        // }
    }
}


pipeline {
    agent any
    tools {
        git 'Default'
        terraform 'terraform'
        maven 'mvn'
    }

    stages {
        stage('Checkout SCM') {
            steps {
                cleanWs()

                git branch: 'main', url: 'https://github.com/yagnasivasai/terraform.git'
                sh 'git clone https://github.com/yagnasivasai/terraform.git'
            }
        }

        stage('Maven build'){
            steps {
                sh '''
                cd task_13_maven
                mvn package
                '''
            }
        }
            

        stage('Building Docker Image'){
            steps{
                sh '''
                    cd task_13_maven
                    echo "alias docker='sudo docker'" >> ~/.bashrc
                    sudo usermod -aG docker $USER
                    sudo chmod 777 /var/run/docker.sock
                    docker build -t yaznasivasai/tomcat:v1 .
                '''
            }
        }

        stage('Pushing Docker Images to DockerHub'){
            steps{
                withCredentials([string(credentialsId: 'DockerHub', variable: 'DockerPasswd')]) {
                sh "docker login -u yaznasivasai -p ${DockerPasswd}"
            }
                sh 'docker push yaznasivasai/tomcat:v1'
            }
            
        }  
       
    }
}


properties([pipelineTriggers([githubPush()])])
 
pipeline {
    /* specify nodes for executing */
    agent {
        label 'github-ci'
    }
 
    stages {
        /* checkout repo */
        stage('Checkout SCM') {
            steps {
                checkout([
                 $class: 'GitSCM',
                 branches: [[name: 'master']],
                 userRemoteConfigs: [[
                    url: 'git@github.com:wshihadeh/rabbitmq_client.git',
                    credentialsId: '',
                 ]]
                ])
            }
        }
         stage('Do the deployment') {
            steps {
                echo ">> Run deploy applications "
            }
        }
    }
 
    /* Cleanup workspace */
    post {
       always {
           deleteDir()
       }
   }
}


pipeline{
    agent any
    tools {
        git 'Default'
    }
    stages{
        stage('Cloning the Repository'){
            steps{
                cleanWs()
                sh 'echo Connecting Private Remote Repository'
                git branch: 'main', credentialsId: 'GJJS', url: 'https://github.com/yagnasivasai/maven-private.git'
                sh 'git clone https://yagnasivasai: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@github.com/yagnasivasai/maven-private.git'
            }
        }
        stage('Build the Dependicies'){
            steps{
                sh 'pip3 install -r requirements.txt'
            }
        }
        stage('Testing the Django Project'){
            steps{
                sh 'python3 manage.py test'
            }
        }
  
        stage('Deploying to Production'){

            input {
                message 'Can we Proceed to Production?'
                ok 'Yes'
            }
            steps{
                sh 'ssh -o StrictHostKeyChecking=no username@192.168.0.1 "source venv/bin/activate; \
                cd polling; \
                git pull https://yagnasivasai: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@github.com/yagnasivasai/maven-private.git; \
                pip install -r requirements.txt --no-warn-script-location; \
                python manage.py migrate; \
                deactivate; \
                sudo systemctl restart nginx; \
                sudo systemctl restart gunicorn" '
                
            }

        }
    }
    
}

node{
    stage('Git Hub Checkout')
    {
        git credentialsId: 'GitHubCredentials', url: 'https://github.com/account/app'
    }
    stage('Build Docker Image')
    {
        bat 'docker build -t imagename/demo:v2 .'
    }
    stage('Push Docker Image Into Docker Hub')
    {
        withCredentials([string(credentialsId: 'Docker_Password', variable: 'Docker_Password')]) 
        {
            bat "docker login -u imagename -p ${Docker_Password}"
        }
        bat 'docker push imagename/demo:v2'
    }
    **stage ('Deployment Into Azure')
    {
        bat 'kubectl apply -f deployment-service.yaml'
    }**

}



pipeline {
    agent any
    stages {
        stage('Example') {
            input {
                message "Let's promote?"
                ok 'Release!'
                parameters {
                    extendedChoice defaultValue: 'blue,green,yellow,blue', description: '', descriptionPropertyValue: 'blue,green,yellow,blue', multiSelectDelimiter: ',', name: 'favColor', quoteValue: false, saveJSONParameterToFile: false, type: 'PT_MULTI_SELECT', value: 'blue,green,yellow,blue', visibleItemCount: 5
                }
            }
            steps {
                echo "Your favorite color is ${favColor}"
            }
            
        }
        stage('Mine'){
            input {
                message 'lets go'
                ok 'Yes'
                parameters {
                extendedChoice description: 'select', multiSelectDelimiter: ',', name: 'color', quoteValue: false, saveJSONParameterToFile: false, type: 'PT_MULTI_SELECT', value: '1,2,3', visibleItemCount: 5
                }
            }
            steps {
                echo "your favorite choice is ${color}"
            }
        }
    }
}





























