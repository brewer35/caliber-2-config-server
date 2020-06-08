

pipeline{

agent any

    environment{
        Register ="damier85/damier-raymond"
        RegisterCrudential ="Mydocker20"
        dockerImage =""


    }
     tools{
     maven 'maven-3'

     }
stages{

    stage ('Clonning from git'){

        steps
        {
            echo "Something"
        }


    }

    stage('Version'){
            steps
                {
                sh 'mvn --version'
                }
          }
    
        stage ("initialize") {
        steps {
        sh '''
        echo "PATH = ${PATH}"
        echo "M2_HOME = ${M2_HOME}"
        '''
        }
        }

    
        stage('Compile the App'){
        steps
           {
            
            sh 'mvn compile'
          }
        }



stage('package the App'){
        steps
        {
            sh "mvn clean package"
        }
    }

stage('Build the image'){

        steps
        {
            script
            {
                dockerImage = docker.build("${Register}:my-image")
            }
        }
}

stage ('Deploy image to DockerHub'){

        steps
        {
                script{
                  docker.withRegistry('', RegisterCrudential)
                    {
                     dockerImage.push()
                    }
                }
            
        }

}

    stage ("Remove unUsed docker image"){
        steps
        {
            sh "docker rmi ${Register}:my-image"
        }
    }



}


}