pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('bootstrap-dockerhub')
        }
    stages {

        stage('Docker Build') {
            steps {
                sh 'docker build -t bahachalbia/catalog  /root/microservice/microservice-demo/microservice-demo-catalog/'
                sh 'docker build -t bahachalbia/customer /root/microservice/microservice-demo/microservice-demo-customer/'
                sh 'docker build -t bahachalbia/eureka /root/microservice/microservice-demo/microservice-demo-eureka-server/'
                sh 'docker build -t bahachalbia/order /root/microservice/microservice-demo/microservice-demo-order/'
                sh 'docker build -t bahachalbia/turbine /root/microservice/microservice-demo/microservice-demo-turbine-server/'
                sh 'docker build -t bahachalbia/zuul /root/microservice/microservice-demo/microservice-demo-zuul-server/'
                 }
        }
          stage('login') {
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u bahachalbia --password-stdin '

            }
        }
        stage('push') {
            steps {
                sh 'docker push bahachalbia/catalog'
                sh 'docker push bahachalbia/customer'
                sh 'docker push bahachalbia/eureka'
                sh 'docker push bahachalbia/order'
                sh 'docker push bahachalbia/turbine'
                sh 'docker push bahachalbia/zuul'

            }
        }
        stage('Docker Logout') {
            steps {
                sh 'docker logout'
            }
        }

    }
}
