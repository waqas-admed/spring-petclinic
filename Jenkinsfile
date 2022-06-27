pipeline {
    agent any
    triggers {
      githubPush()
    }
    tools {
        maven "maven3"
        jdk "java11"


    }
    stages {
        stage('Config') {
            steps {
                echo "PATH = ${M2_HOME}/bin:${PATH}"
                echo "M2_HOME = ${M2_HOME}"
                git url: 'https://github.com/spring-projects/spring-petclinic.git', branch: 'main',
                 credentialsId: 'github'

            }
        }

        stage('Compile') {
            steps {
                sh '$WORKSPACE/mvnw -DskipTests clean package'
                echo "sleep 5"
            }
        }
        
        
        stage('Test-cases') {
            steps {
                sh 'mvn test'
                echo "sleep 5"
                sh '$WORKSPACE/mvnw test'
            }
        }

        
        
        

        stage('Creating-container') {
            steps {
                echo "Running test-cases in container..."
                sh '$WORKSPACE/mvnw spring-boot:build-image'
            }
        }

        

    }
    post { 
        always { 
            echo 'always run this step'
        }
    }
}
