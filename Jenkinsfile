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
                scp -i \$KEYFILE src/main.go vagrant@172.28.128.3:~/
            """
        }
    }
}