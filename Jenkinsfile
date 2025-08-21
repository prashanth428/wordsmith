pipeline{
        agent any
        stages{   
                stage('travy-FS-scan'){
                    agent {
                        docker{
                            image 'aquasec/trivy'
                            reuseNode true
                            }
                    steps{
                        sh 'travy --version'
                        sh 'travy fs .'

                    }                
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
                        '''
                    }
                }
                stage('compile-web'){

                    steps{
                        echo 'this is the compail stage of web'
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