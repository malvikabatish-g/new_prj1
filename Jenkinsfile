pipeline {
    agent any

    stages {

        stage('Clone') {
            steps {
                sh '''
                rm -rf repo
                git clone -b main https://github.com/malvikabatish-g/new_prj1.git repo
                '''
            }
        }

        stage('Build Image') {
            steps {
                sh '''
                cd repo
                docker build -t html-site .
                '''
            }
        }

        stage('Verify Image') {
            steps {
                sh '''
                docker images | grep html-site
                '''
            }
        }
        stage('Deploy') {
    steps {
        sh '''
        docker rm -f html-site-container || true
        docker run -d \
          --name html-site-container \
          -p 8081:80 \
          html-site
        '''
    }
}
    }
}
