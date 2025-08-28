pipeline{
        agent any
        stages{   
                stage('travy-FS-scan'){
                    steps{
                        sh 'docker run aquasec/trivy fs .'

                    }                
                }
                

                stage('Compaile'){
                parallel{
                    stage('compile-api'){
                        agent {
                            docker {
                                image 'maven:3.8.5-openjdk-17'
                                reuseNode true
                            }
                        }
                    steps{
                        sh '''
                            cd api
                            mvn compile
                            mvn test
                            cd ..
                        '''
                    }
                }
                stage('compile-web'){
                            environment {
            GOCACHE = "${WORKSPACE}/.go-cache" // Or any other writable path within the workspace
        }
                    agent{
                        docker{
                            image 'golang:alpine3.21'
                            args '-v $HOME/.ssh:/root/.ssh'
                            reuseNode true
                        }
                    }
                    steps{
                        sh '''
                        go version
                        cd web
                        go build dispatcher.go
                        '''
                    }
                }
                }
                }
                stage('test'){
                    steps{
                        echo 'this is the test stage'
                        }
                }
                stage('sonarqube'){
                    steps{
                        echo 'This is the sonarqube scan stage'
                    }
                }
                stage('travy'){
                    steps{
                        echo 'this is travy scan stage'
                    }                
                }
                stage('qualitygate'){
                    steps{
                        echo ' this is the quality gate stage'
                    }
                }
                stage('Build'){
                    steps{
                        echo ' this is the build stage'
                    }
                }
                stage('create athe docker image'){
                    steps{
                        echo ' this is the docker build stage'
                    }
                }

        }
}