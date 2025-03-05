pipeline {
    agent any
 
    stages {
        stage('Clone Repository') {
            steps {
                git url: 'https://github.com/Pradhisha-N/python_jenkins.git', branch: 'main'
            }
        }
 
        stage('Set Up Virtual Environment') {
            steps {
                sh 'python3 -m venv venv'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '. venv/bin/activate && pip install --upgrade pip && pip install -r requirements.txt'
            }
        }

 
        stage('Run Tests') {
            steps {
                // Run tests inside the virtual environment
                sh '. venv/bin/activate && PYTHONPATH=$PWD pytest test/'
            }
        }
 
        stage('Build Artifact') {
            steps {
                // Build the artifact inside the virtual environment
                sh '. venv/bin/activate && python setup.py sdist'
            }
        }
 
        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'dist/*.tar.gz', fingerprint: true
            }
        }
    }
}
