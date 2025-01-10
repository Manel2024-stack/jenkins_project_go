pipeline {
    agent {
        node {
            label 'jenkins-node'
        }
    }

    stages {
        stage('Continuous integration') {
            steps {
                git branch: 'main', url: 'https://github.com/fredericEducentre/jenkins_project_go.git'
            }
        }
        stage('build') {
            steps {
                sh "docker build . -t current_time_go"
                sh "docker run --rm current_time_go"
            }
        }
         stage('Contrôle qualité') {
            steps {
                sh '''
                sonar-scanner \
                  -Dsonar.projectKey=jenkins_project_go \
                  -Dsonar.sources=. \
                  -Dsonar.host.url=http://192.168.232.132:9000 \
                  -Dsonar.token=sqp_c7c927a88826fcadb56a458be78c8c4dbc56c501
                '''
            }
        }
    }
}
