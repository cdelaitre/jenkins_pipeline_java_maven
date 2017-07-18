stage ('Build') {
  // Asking for an agent with label 'docker-cloud'
  node {
    checkout scm
    // Let's retrieve the SHA-1 on the last commit (to identify the version we build)
    sh('git rev-parse HEAD > GIT_COMMIT')
    git_commit=readFile('GIT_COMMIT')
    short_commit=git_commit.take(7)
    // Let's build the application inside a Docker container
    docker.image('kmadel/maven:3.3.3-jdk-8').inside('-v /data:/data') {
        sh "mvn -Dmaven.repo.local=/data/mvn/repo -DGIT_COMMIT='${short_commit}' -DBUILD_NUMBER=${env.BUILD_NUMBER} -DBUILD_URL=${env.BUILD_URL} clean package"
    }
  }
}
