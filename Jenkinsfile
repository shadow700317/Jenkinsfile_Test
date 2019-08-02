pipeline {
    agent {
        label "maven"
    }
    stages  {
        
        stage('CheckOut') {
			steps {
				script {
    				git url: 'http://172.16.20.31:1080/aztldemo/aztl-demo-zh.git', branch: 'master'
    			}
			}
		}

        stage("Complier") {
            steps {
                echo "建構中..."
              	sh 'mvn package -Dmaven.test.skip=true' // mvn 示例
                archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true // 收集建構JAR檔             	
                echo "建構完成."
            }
        }

        stage("測試") {
            steps {
                echo "單元測試中..."
                // 使用JUnit進行單元測試
                sh 'mvn test' // mvn 示例
                echo "單元測試完成."
                junit '**/target/surefire-reports/*.xml' // 收集單元測試報告調用進程
            }
        }
		stage("部屬確認") {
            steps {
                input message: 'Deploy', ok: 'Yes'
            }
            
        }
        stage("部署") {
            steps {
                echo "部署中..."
                echo "部署完成"
            }
        }
		
    }
}
