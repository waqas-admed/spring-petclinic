pipeline {
    agent any
    triggers {
      githubPush()
    }
    tools {
        maven "maven3"
        jdk "java11"
        dockerTool 'docker'

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
                echo "PATH = ${dockerTool}/bin:${PATH}"
                sh 'mvn -DskipTests clean package'
                sh '$WORKSPACE/mvnw spring-boot:build-image'
            }
        }



    }
    post { 
        always { 
            echo 'I will always say Hello again!'
        }
    }
}
