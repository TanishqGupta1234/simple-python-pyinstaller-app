pipeline {
    // 'None' in the agent section means that no global agent will be allocated for the entire pipeline.
    agent none
    stages {
        stage('Build') {
            agent {
                docker {
                    // This image parameter downloads the python:2-alpine Docker image
                    // and runs this image as a separate container.
                    image 'python:2-alpine'
                }
            }
            steps {
                // Run the Python command to compile your application
                sh 'python -m py_compile sources/add2vals.py sources/calc.py'
                
                // Stash the Python source code and compiled bytecode files
                stash(name: 'compiled-results', includes: 'sources/*.py*')
            }
        }
    }
}
