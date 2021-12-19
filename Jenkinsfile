pipeline {
  agent none
  stages {
    stage('Build') {
      agent {
        docker {
          image 'golang:1.14.2' // 构建镜像
          args '-e GOPROXY=https://goproxy.io -e GO111MODULE=on -e CGO_ENABLED=0 -e GOOS=linux -e GOARCH=amd64 -v /var/jenkins_home/workspace/go-web-docker:/go/src/app'
        }
      }
      steps {
        sh 'go build -o app' // 构建app可执行程序
      }
    }
    stage('Deploy') {
      agent any
      steps {
        sh 'docker restart webapp' // 重启name为webapp的容器
      }
    }
  }
}