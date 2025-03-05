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
                // Ensure python3-venv is available
                sh 'python3 -m venv venv'
                sh '. venv/bin/activate' // Activate the virtual environment
            }
        }
 
        stage('Install Dependencies') {
            steps {
                // Install dependencies inside the virtual environment
                sh '. venv/bin/activate && pip install -r requirements.txt'
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
