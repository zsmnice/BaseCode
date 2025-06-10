pipeline {
    agent any

    environment {
        JAVA_HOME = '/usr/lib/jvm/java-1.8.0-openjdk'
        MAVEN_HOME = '/usr/share/maven'
        PATH = "${env.MAVEN_HOME}/bin:${env.PATH}"
    }

    stages {
        stage('拉取代码') {
            steps {
                git branch: 'main', url: 'https://github.com/zsmnice/BaseCode.git'
            }
        }

        stage('编译打包') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('构建并重启 ruoyi-admin 服务') {
            steps {
                sh '''
                    docker compose -p ruoyi down || true
                    docker compose -p ruoyi up -d --build
                '''
            }
        }
    }
}
