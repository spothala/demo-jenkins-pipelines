node {
    stage('SCP'){
        withCredentials([
          usernamePassword(credentialsId: "vagrant",
          keyFileVariable: 'KEYFILE', usernameVariable: 'USERNAME')
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