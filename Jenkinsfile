    pipeline{

        agent any

        stages {

            stage('Git Checkout'){

                steps{

                    script{

                        git branch: 'main', url: 'https://github.com/vikash-kumar01/demo-counter-app.git'
                    }
                }
            }

            stage('UNIT Testing'){

                steps {
                   sh 'mvn test'
            }
            }

            stage ('Integration Testing'){
                steps {
                    sh 'mvn verify -DskipUnitTests'
                }
            }

            stage ('Maven Build'){
                steps{
                    sh 'mvn clean install'
                }
            }

            stage ('static code analysis'){
                steps{
                    script{
                         withSonarQubeEnv(credentialsId: 'Jenkins_Auth') {        
                            sh 'mvn clean package sonar:sonar'
                    }
                    }
                   
                }
            }


             stage ('Quality Gate Status'){
                steps{
                    script{
                         waitForQualityGate abortPipeline: false, credentialsId: 'Jenkins_Auth'
                    }
                   
                }
            }
        }
    }