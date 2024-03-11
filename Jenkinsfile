pipeline {
    agent any
    environment {
        SCANNER_HOME = tool 'sonar'
    }
    stages {
        stage('git checkout') {
            steps {
                git credentialsId: 'github', url: 'https://github.com/kesav38/10-Tier-Webapp-Microservices.git'
            }
        }
        stage('SonarQube') {
            steps {
                withSonarQubeEnv('sonarserver') {
                     sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectKey=10-Tier -Dsonar.ProjectName=10-Tier -Dsonar.java.binaries=. ''' 
                }
            }
        }
        stage('adservice') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'kesav38', toolName: 'docker') {
                        dir('/var/lib/jenkins/workspace/10microservice/src/adservice') {
                            sh 'docker build -t kesav38/adservice:${BUILD_NUMBER} .'
                            sh 'docker push kesav38/adservice:${BUILD_NUMBER}'
                            sh 'docker rmi kesav38/adservice:${BUILD_NUMBER}'
                        }
                    }
                }
            }
        }
        stage('cartservice') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'kesav38', toolName: 'docker') {
                        dir('/var/lib/jenkins/workspace/10microservice/src/cartservice/src/') {
                            sh 'docker build -t kesav38/cartservice:${BUILD_NUMBER} .'
                            sh 'docker push kesav38/cartservice:${BUILD_NUMBER}'
                            sh 'docker rmi kesav38/cartservice:${BUILD_NUMBER}'
                        }
                    }
                }
            }
        }
        stage('checkoutservice') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'kesav38', toolName: 'docker') {
                        dir('/var/lib/jenkins/workspace/10microservice/src/checkoutservice/') {
                            sh 'docker build -t kesav38/checkoutservice:${BUILD_NUMBER} .'
                            sh 'docker push kesav38/checkoutservice:${BUILD_NUMBER}'
                            sh 'docker rmi kesav38/checkoutservice:${BUILD_NUMBER}'
                        }
                    }
                }
            }
        }
        stage('currencyservice') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'kesav38', toolName: 'docker') {
                        dir('/var/lib/jenkins/workspace/10microservice/src/currencyservice/') {
                            sh 'docker build -t kesav38/currencyservice:${BUILD_NUMBER} .'
                            sh 'docker push kesav38/currencyservice:${BUILD_NUMBER}'
                            sh 'docker rmi kesav38/currencyservice:${BUILD_NUMBER}'
                        }
                    }
                }
            }
        }
        stage('emailservice') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'kesav38', toolName: 'docker') {
                        dir('/var/lib/jenkins/workspace/10microservice/src/emailservice/') {
                            sh 'docker build -t kesav38/emailservice:${BUILD_NUMBER} .'
                            sh 'docker push kesav38/emailservice:${BUILD_NUMBER}'
                            sh 'docker rmi kesav38/emailservice:${BUILD_NUMBER}'
                        }
                    }
                }
            }
        }
        stage('frontend') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'kesav38', toolName: 'docker') {
                        dir('/var/lib/jenkins/workspace/10microservice/src/frontend/') {
                            sh 'docker build -t kesav38/frontend:${BUILD_NUMBER} .'
                            sh 'docker push kesav38/frontend:${BUILD_NUMBER}'
                            sh 'docker rmi kesav38/frontend:${BUILD_NUMBER}'
                        }
                    }
                }
            }
        }
        stage('loadgenerator') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'kesav38', toolName: 'docker') {
                        dir('/var/lib/jenkins/workspace/10microservice/src/loadgenerator/') {
                            sh 'docker build -t kesav38/loadgenerator:${BUILD_NUMBER} .'
                            sh 'docker push kesav38/loadgenerator:${BUILD_NUMBER}'
                            sh 'docker rmi kesav38/loadgenerator:${BUILD_NUMBER}'
                        }
                    }
                }
            }
        }
        stage('paymentservice') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'kesav38', toolName: 'docker') {
                        dir('/var/lib/jenkins/workspace/10microservice/src/paymentservice/') {
                            sh 'docker build -t kesav38/paymentservice:${BUILD_NUMBER} .'
                            sh 'docker push kesav38/paymentservice:${BUILD_NUMBER}'
                            sh 'docker rmi kesav38/paymentservice:${BUILD_NUMBER}'
                        }
                    }
                }
            }
        }
        stage('productcatalogservice') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'kesav38', toolName: 'docker') {
                        dir('/var/lib/jenkins/workspace/10microservice/src/productcatalogservice/') {
                            sh 'docker build -t kesav38/productcatalogservice:${BUILD_NUMBER} .'
                            sh 'docker push kesav38/productcatalogservice:${BUILD_NUMBER}'
                            sh 'docker rmi kesav38/productcatalogservice:${BUILD_NUMBER}'
                        }
                    }
                }
            }
        }
        stage('recommendationservice') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'kesav38', toolName: 'docker') {
                        dir('/var/lib/jenkins/workspace/10microservice/src/recommendationservice/') {
                            sh 'docker build -t kesav38/recommendationservice:${BUILD_NUMBER} .'
                            sh 'docker push kesav38/recommendationservice:${BUILD_NUMBER}'
                            sh 'docker rmi kesav38/recommendationservice:${BUILD_NUMBER}'
                        }
                    }
                }
            }
        }
        stage('shippingservice') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'kesav38', toolName: 'docker') {
                        dir('/var/lib/jenkins/workspace/10microservice/src/shippingservice/') {
                            sh 'docker build -t kesav38/shippingservice:${BUILD_NUMBER} .'
                            sh 'docker push kesav38/shippingservice:${BUILD_NUMBER}'
                            sh 'docker rmi kesav38/shippingservice:${BUILD_NUMBER}'
                        }
                    }
                }
            }
        }
        stage('K8-Deploy') {
            steps {
                sh 'aws eks update-kubeconfig --name my-eks2'
                sh 'kubectl apply -f deployment10tierwebapp.yaml -n web'
                sh 'kubectl get pods'
                sh 'kubectl get svc'
            }
        }
    }
}
