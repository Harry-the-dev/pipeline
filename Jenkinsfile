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
        }
    }