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
                // sh 'docker cp filebeat.yml f4ed25d50e25:/filebeat.yml && docker cp entrypoint.sh f4ed25d50e25:/entrypoint.sh'
                // sh '''
                //     docker exec f4ed25d50e25 /bin/bash && \
                //     ls -al && \
                //     apt-get && \
                //     apt-get update && apt-get install filebeat && \
                //     cp filebeat.yml /etc/filebeat/filebeat.yml && \
                //     chmod +x /entrypoint.sh && \
                //     ./entrypoint.sh
                //     '''
                sh 'docker build -t jiananlin:test jiananlin:test'
                sh 'docker run jiananlin:test'
            }
        }
    }
}
