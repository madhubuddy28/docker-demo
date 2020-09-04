node {
def commit_id
stage('Preparation') {
checkout scm
sh "git rev-parse --short HEAD > .git/commit-id"
commit_id = readFile('.git/commit-id').trim()
}
stage('test') {
nodejs(nodeJSInstallationName: 'nodejs') {
sh 'npm install --only=dev'
sh 'npm test'
}
}
stage ('docker build/push') {
docker.withRegistry('https://hub.docker.com/', '621aa701-f996-4797-84ec-0a6cbba01505') {
def app = docker.build("madhubuddy28/docker-demo:${commit_id}", '.').push()
}}
}
