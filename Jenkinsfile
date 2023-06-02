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

            stage ('Upload Jar file to nexus'){
                steps{
                    script{
                        nexusArtifactUploader artifacts: 
                        [
                            [
                                artifactId: 'springboot',
                                classifier: '',
                                file: 'target/Uber.jar', 
                                type: 'jar'
                            ]
                        ], 
                        credentialsId: 'nexus-login', 
                        groupId: 'com.example', 
                        nexusUrl: 'localhost:8081', 
                        nexusVersion: 'nexus3', 
                        protocol: 'http', 
                        repository: 'demoapp-release', 
                        version: '1.0.0'
                    }
                }

            }
        }
    }