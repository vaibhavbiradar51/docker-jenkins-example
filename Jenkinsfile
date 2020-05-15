node {
    def app

    stage('Clone repository') {
        checkout scm
    }

    stage('Build image') {
        app = docker.build("djangobasic:${env.BUILD_ID}")
    }

    stage('Run Test Django') {
        app.inside {
            sh 'python manage.py test'
        }
    }

    stage('Clear old version') {
        echo "Running source code in a fully containerized environment..."    
        sh 'docker-compose down -v'
    }

    stage('Deploy Source Code') {
        echo "Running source code in a fully containerized environment..."    
        sh 'docker-compose up -d --build'
    }
}