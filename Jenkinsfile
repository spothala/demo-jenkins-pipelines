node {
    stage('SCP'){
        withCredentials(bindings: [
          sshUserPrivateKey(credentialsId: "vagrant-key",
          keyFileVariable: 'KEYFILE')
        ]) {
            checkout scm
            sh """#!/bin/bash
                set -eo pipefail
                ls -altr
                scp -i \$KEYFILE -o StrictHostKeyChecking=no src/main.go vagrant@172.28.128.3:~/
                ssh -i \$KEYFILE -o StrictHostKeyChecking=no vagrant@172.28.128.3 'source /etc/profile && go run main.go'
            """
        }
    }
}