pipeline {
    agent any 
    stages {
        stage('Configure logstash es kibana on host') {
            steps {
                echo 'Hello world!' 
            }
        }
        stage('Configure filebeat and generate log on slave') {
            agent {
                label 'slave-1'
            }
            steps {
                script{
                    for(int i = 0; i < 20; ++i) {
                        echo "this is the ${i} time."
                        echo "-------------------------------------------"
                        if(i % 2 == 0) {
                            echo "Also this is an even number."
                            echo "-----------------------------------------------"
                        }
                        sleep(0.5);
                    }
                }
                sh 'pwd'
                sh 'ls'
            }
        }
    }
}
