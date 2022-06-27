pipeline {
    agent any
    triggers {
      githubPush()
    }

    stages {
        stage('Config') {
            steps {
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
                sh '$WORKSPACE/mvnw test'
            }
        }

        
        
        

        stage('Creating-container') {
            steps {
                echo "creating container"
                echo "Running test-cases in container..."
                sh '$WORKSPACE/mvnw spring-boot:build-image'
            }
        }

        

    }
    post { 
        always { 
            junit '**/target/surefire-reports/TEST-*.xml'
            archive 'target/*.jar'

        }
    }
}
