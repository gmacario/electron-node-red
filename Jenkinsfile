pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        // stage('Install') {
        //     agent {
        //         docker {
        //             image 'node:12.13.1'
        //             reuseNode true
        //         }
        //     }
        //     steps {
        //         sh 'npm i'
        //     }
        // }
        stage('Build via electron-builder') {
            agent {
                dockerfile {
                    label 'docker && linux'
                    dir 'ci/jenkins'
                    reuseNode true
                }
            }
            steps {
              sh 'node --version'
              sh 'npm --version'
              // sh 'yarn --version'
              // sh 'yarn'

              // sh 'yarn dist'
              // sh 'ls -la dist/'

              // sh 'yarn dist --windows msi:ia32'

              sh 'npm install'
              sh './node_modules/.bin/electron-builder --windows'
              sh 'ls -la dist/'

              archiveArtifacts(artifacts: 'dist/*', allowEmptyArchive: true, fingerprint: true)
            }
        }
    }
}
