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
              sh 'yarn --version'

              sh 'yarn'

            //   sh 'yarn dist'
            //   sh 'ls -la dist/'

              // sh 'npm i -g electron-zip-packager'
              // sh 'electron-zip-packager app/ "Accessidys" --asar=true --out=..\\dist\\win --platform=win32 --arch=ia32 --icon="styles/images/favicon.ico" --ignore=builder.json --ignore=README.md --overwrite'
            
              sh 'yarn dist --windows msi:ia32'
              sh 'ls -la dist/'

              archiveArtifacts(artifacts: 'dist/*', allowEmptyArchive: true, fingerprint: true)
            }
        }
    }
}