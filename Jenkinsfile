pipeline {
    agent none
    stages {
        stage('Build') {
            agent {
                docker {
                    image 'python:3-alpine'  // Use Python 3 instead of deprecated Python 2
                    args '--user=root'      // Avoid permission issues
                }
            }
            steps {
                script {
                    // Debug: List source files before compilation
                    sh 'ls -al sources || echo "Sources directory missing!"'

                    // Ensure Python source files exist before running compilation
                    sh '[ -f sources/add2vals.py ] && [ -f sources/calc.py ] || (echo "Source files missing!" && exit 1)'

                    // Compile Python files
                    sh 'python -m py_compile sources/add2vals.py sources/calc.py'

                    // Debug: Verify compiled files exist
                    sh 'ls -al sources/*.py* || echo "Compiled files missing!"'

                    // Stash compiled files for later use
                    stash(name: 'compiled-results', includes: 'sources/*.py*')
                }
            }
        }
    }
}
