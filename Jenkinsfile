//trigger test
properties([pipelineTriggers([githubPush()])])
node {
    def env = params.cert
    stage('checkout'){
    checkout([$class: 'GitSCM', branches: [[name: '*/master']],
    userRemoteConfigs: [[credentialsId: 'github', url: 'https://github.com/saiganeshsunkari/elk-demo.git']]])
    }
    stage('kube-config') {
        sh "echo $env"
     withKubeConfig(
        [credentialsId: 'elk-kubernetes', serverUrl: 'https://172.31.66.235:8443', caCertificate: '$env']
    ){
      //sh 'kubectl config view'
      sh 'ls -la'
      sh 'kubectl get pods -n test --insecure-skip-tls-verify'
      //sh 'kubectl apply -f es-dep.yaml --insecure-skip-tls-verify'
      //sh 'kubectl delete -f elk-demo/es-dep.yaml --insecure-skip-tls-verify'
    } 
    }
    
}
