pipeline {
    agent any
    stages {
        agent {
            docker {
                image 'python3.7'
                args '-v /tmp/resources:/tmp/resources'
        }
        stage('Package resources'){
            steps {
                sh 'python3 -m venv venv'
                sh 'venv/bin/pip3 install -r requirements.txt'
                sh 'echo hello > /tmp/resources/hello'
                // sh 'cd venv/lib/python3.6/site-packages'
                // sh 'zip -r $OLDPWD/ImageResize.zip .'
                // sh 'cd $OLDPWD'
                // sh 'zip ImageResize.zip image_resize.py'
                // sh 'mkdir /tmp/resources'
                // sh 'cp playbooks/aws_role/policy.json /tmp/resources'
                // sh 'cp ImageResize.zip /tmp/resources'
            }
        }
        stage('Deploy resources') {
            agent {
                docker {
                    image 'python3.7'
                    args '-v /tmp/resources:/tmp/resources'
                    reuseNode true
                }
            }
            steps {
                sh 'echo /tmp/resources/hello'
                sh 'sudo pip3 install boto3'
                sh 'sudo pip3 install git+https://github.com/ansible/ansible.git@devel'
                sh 'sudo pip3 install opera'

                // sh 'opera deploy resize resize_service_opera.yml'
            }
        }

        stage('Test functionality') {
            agent {
                docker {
                    reuseNode true
                }
            }
            steps {
                sh 'echo Install awscli'
                sh 'sudo pip3 install awscli'

                // sh 'echo Upload image'
                // sh 'curl https://www.dogsnsw.org.au/media/img/BrowseAllBreed//Irish-Setter.jpg > $IMAGE'
                // sh 'aws s3 mv $IMAGE s3://radon-img3-naesheim'

                // sh 'echo aws s3 ls radon-img3-naesheim-resized'
            }
        }
    }
}