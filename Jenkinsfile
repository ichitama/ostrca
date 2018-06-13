def jenkins_path = "/var/lib/jenkins"
def tf_path      = "${jenkins_path}/terraform/build"
def ansible_path = "${jenkins_path}/ansible"
def terraform    = "/usr/local/bin/terraform"

def cgreen_name  = ""

node {
    stage('scm'){
        checkout scm
    }

    stage('build & test'){
        sh "Building code and test"

    }

    stage('Confirm current green server'){
        //現在のGreenサーバの情報(AWS関係)を取得
        dir("${tf_path}"){
            id = sh returnStdout: ture, script: "${terraform} state showterraform state show aws_lb_target_group_attachement.green_attach | grep target_id | awk '{print ${option}}'"
            
            result = sh returnStdout: true,script: "${terraform} state show aws_instance.2anet_server1 | grep ${id}"

            if(result == ""){
                cgreen_name = "2anet_server2"
            }else{
                cgreen_name = "2anet_server1"
            }

            }
        sh "echo ${id}"
    
    }

    stage('Destroy of the current green server'){
        //現在のGreenサーバを破棄

    }

    stage('Create new blue server instance'){
        //新しいBlueサーバのインスタンス作成
        //旧Greenサーバと同じTargetGroupに接続
    }

    stage('Provisioning for new blue server'){
        //Ansibleを使用して新しいBlueサーバを
    }

    stage('Execute test for new blue server'){
        sh "echo 'server test'"
    }

    stage('Switch the new blue server'){

    }

}