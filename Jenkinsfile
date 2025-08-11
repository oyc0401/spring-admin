pipeline {
    agent any

    environment {
        REMOTE_HOST = 'ubuntu@43.201.125.168'          // EC2 접속 계정/주소
        REMOTE_PATH = '/home/ubuntu/admin-docker' // docker-compose.yml 있는 경로
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Deploy Jenkins Container') {
            steps {
                sshagent(credentials: ['ec2-ssh-key']) { // Jenkins Credentials ID
                    sh """
                        ssh -o StrictHostKeyChecking=no $REMOTE_HOST '
                            set -e

                            # 1) 디렉토리 생성 & compose 파일 복사
                            mkdir -p $REMOTE_PATH
                        '
                        scp -o StrictHostKeyChecking=no docker-compose.yaml $REMOTE_HOST:$REMOTE_PATH/docker-compose.yml

                        # 2) 컨테이너 재시작
                        ssh -o StrictHostKeyChecking=no $REMOTE_HOST '
                            cd $REMOTE_PATH
                            # 필요시 기존 컨테이너 내리기
                            docker compose down || true
                            # 새로 올리기
                            docker compose up -d
                            docker ps --filter "name=jenkins"
                        '
                    """
                }
            }
        }
    }
}
