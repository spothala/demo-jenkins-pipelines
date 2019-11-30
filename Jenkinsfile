node('SCP') {
    checkout scm
    sh """#!/bin/bash
        set -eo pipefail
        ls -altr
        scp src/main.go vagrant:~/
    """
}