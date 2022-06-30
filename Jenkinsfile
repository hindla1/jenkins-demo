pipeline{
    agent any;
    stages{
        
        stage('GitCheckout'){
            
            steps{
                echo 'Checking out my code'
                git credentialsId: '5ba20f73-33f1-4a32-a4b2-539efd18facf', url: 'https://github.com/hindla1/jenkins-demo.git'
            }
        }
        
        stage('build'){
            steps {
                echo 'building the artifact'
                sh '/home/ec2-user/apache-ant-1.10.12/bin/ant -f ant.xml'
            }
            
        }
       stage('parallel run'){
               parallel{
                    stage('test-1'){
                          steps {
                                echo "test cases are passed"
                                sleep 20
                            }
                        }
                    stage('test-2'){
                                steps {
                                        echo "test cases are passed"
                                        sleep 20
                                        }
                            }
                }
        }
        stage('deploy'){
            steps{
                echo 'Deploiyment has been started..!'
                deploy adapters: [tomcat8(credentialsId: '7f99369c-5136-4f8f-b4a1-1e964db90dbc', path: '', url: 'http://44.205.15.252:8080/')], contextPath: '/buildDemo', war: '**/*.war'
            }
        }
        
    }
}
