pipeline{
        agent any
        stages{
                stage('Compaile'){
                stage('compile-api'){
                    steps{
                        echo 'this is the compail stage'
                    }
                }
                stage('compile-web'){
                    steps{
                        echo 'this is the compail stage'
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