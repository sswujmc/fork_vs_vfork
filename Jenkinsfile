node {
    def app
    stage('Clone repository') {
            git branch: 'main', url: 'https://github.com/sswujmc/fork_vs_vfork.git'
    }
    stage('Build image') {
        app = docker.build("sswujmc/test")
    }
    stage('Test image') {
        app.inside {
            sh 'make test'
        }
    }
    stage('Push image') {
        docker.withRegistry('https://registry.hub.docker.com', 'sswujmc') {
           app.push("${env.BUILD_NUMBER}")
           app.push("latest")
        }
    }
}
