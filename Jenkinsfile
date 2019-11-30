node {
    stage('Build'){
        checkout scm
        sh """#!/bin/bash
            set -eo pipefail
            ls -altr
            docker build -t hello:1.0 .            
        """
    }
    stage('Build'){
        sh """
            #!/bin/bash
            set -eo pipefail
            docker run --rm --name gohello -p 3001:3001 hello:1.0
        """
    }
}