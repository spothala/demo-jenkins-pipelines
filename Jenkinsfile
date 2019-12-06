def label = "worker-${UUID.randomUUID().toString()}"

podTemplate(
    label: label, 
    containers: [
        containerTemplate(name: 'docker', image: 'docker', command: 'cat', ttyEnabled: true),
        containerTemplate(name: 'kubectl', image: 'lachlanevenson/k8s-kubectl:v1.8.8', command: 'cat', ttyEnabled: true)
    ],
    volumes: [
        hostPathVolume(mountPath: '/var/run/docker.sock', hostPath: '/var/run/docker.sock')
]) {
    node(label) {
        stage('Build'){
            container('docker') {
                checkout scm
                sh """#!/bin/sh -x
                set -eo pipefail
                ls -altr
                docker build -t hello:1.0 .
                docker run -d --rm --name gohello -p 3002:3001 hello:1.0            
                """
            }
        }
    }
}