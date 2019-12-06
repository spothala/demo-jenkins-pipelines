def label = "worker-${UUID.randomUUID().toString()}"

podTemplate(
    label: label, 
    containers: [
        containerTemplate(name: 'docker', image: 'docker', command: 'cat', ttyEnabled: true),
        containerTemplate(name: 'kubectl', image: 'lachlanevenson/k8s-kubectl:v1.16.3', command: 'cat', ttyEnabled: true)
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
                docker build -t hello:2.0 .
                """
            }
            container('kubectl') {
                checkout scm
                sh """#!/bin/sh -x
                set -eo pipefail
                kubectl apply -f k8s.yaml
                kubectl get pods
                kubectl get svc
                """
            }
        }
    }
}