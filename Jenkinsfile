pipeline{
        agent any
        environment{
            SCANNER_HOME=tool 'SonarQube_Scanner'
        }
        stages{   
                stage('travy-FS-scan'){
                    steps{
                        sh 'docker run aquasec/trivy repo ./'
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
                    parallel{
                stage('sonarqube'){
                    steps{
                        withSonarQubeEnv('SonarQube_Server'){
                            sh '''
                                echo $SonarQube_Server
                                ${SCANNER_HOME}/bin/sonar-scanner --version
                                ${SCANNER_HOME}/bin/sonar-scanner -Dsonar.projectName=wordsmith -Dsonar.projectKey=wordsmith -Dsonar.sources=. -Dsonar.java.bninaries=./api/
                            '''

                        }
                    }
                }
                stage('travy'){
                    steps{
                   sh 'docker run aquasec/trivy repo ./'     
                    }                
                }
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