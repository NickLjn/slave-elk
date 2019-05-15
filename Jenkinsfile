// node {
//     stage('echo in host') {
//         echo 'Hello world!' 
//     }
//     stage('gen data and send to influxdb') {
//         node('slave-1') {
//             try {
//                 for(int i = 0; i < 20; ++i) {
//                     echo "this is the ${i} time."
//                     echo "-------------------------------------------"
//                     if(i % 2 == 0) {
//                         echo "Also this is an even number."
//                         echo "-----------------------------------------------"
//                     }
//                     sleep(0.5);
//                 }
//                 sh 'pwd'
//                 sh 'ls'
//                 // sh 'docker cp filebeat.yml f4ed25d50e25:/filebeat.yml && docker cp entrypoint.sh f4ed25d50e25:/entrypoint.sh'
//                 sh '''
//                     docker exec f4ed25d50e25 /bin/bash && \
//                     ls -al && \
//                     apt-get && \
//                     apt-get update && apt-get install filebeat && \
//                     cp filebeat.yml /etc/filebeat/filebeat.yml && \
//                     chmod +x /entrypoint.sh && \
//                     ./entrypoint.sh
//                     '''
//                 // sh 'docker build -t jiananlin:test .'
//                 // sh 'docker run -it jiananlin:test'
//             }
//             catch(Exception e) {
//                 step([$class: 'InfluxDbPublisher', customData: null, customDataMap: null, customPrefix: null, target: 'http://localhost:8086,jenkins_data'])
//             }
//         }  
//     }
//     // post {
//     //     always {
//     //         step([$class: 'InfluxDbPublisher', customData: null, customDataMap: null, customPrefix: null, target: 'http://localhost:8086,jenkins_data'])
//     //     }
//     // }
// }
pipeline {
    agent any 
    stages {
        stage('echo on host') {
            steps {
                echo 'Hello world!' 
            }
        }
        stage('generate log and send to influxdb') {
            agent {
                label 'slave-1'
            }
            steps {
                script{
                    try {
                        for(int i = 0; i < 20; ++i) {
                            echo "this is the ${i} time."
                            echo "-------------------------------------------"
                            if(i % 2 == 0) {
                                echo "Also this is an even number."
                                echo "-----------------------------------------------"
                            }
                            sleep(0.5);
                        }
                    }catch(Exception e) {
                        step([$class: 'InfluxDbPublisher', customData: null, customDataMap: null, customPrefix: null, target: 'http://172.17.0.3:8086,jenkins_data'])
                    }
                }
                sh 'pwd'
                sh 'ls'
                sh 'docker cp filebeat.yml f4ed25d50e25:/filebeat.yml && docker cp entrypoint.sh f4ed25d50e25:/entrypoint.sh'
                sh '''
                    docker exec f4ed25d50e25 /bin/bash && \
                    ls -al && \
                    apt-get && \
                    apt-get update && apt-get install filebeat && \
                    cp filebeat.yml /etc/filebeat/filebeat.yml && \
                    chmod +x /entrypoint.sh && \
                    ./entrypoint.sh
                    '''
                // sh 'docker build -t jiananlin:test .'
                // sh 'docker run -it jiananlin:test'
            }
        }
    }
    // post{
    //     always {
    //         step([$class: 'InfluxDbPublisher', customData: null, customDataMap: null, customPrefix: null, target: 'http://172.17.0.3:8086,jenkins_data'])
    //     }
    // }
}
