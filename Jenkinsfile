pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/olehskomorokha/SP-Task4.git', credentialsId: 'accsess_for_jenkins'
            }
        }
        
        stage('Build') {
            steps {
                script{
                    try{
                        bat '"C:\\Program Files\\Microsoft Visual Studio\\2022\\Community\\MSBuild\\Current\\Bin\\MSBuild.exe" Skomoroha-Test.sln /t:Build /p:Configuration=Release'
                    }
                    catch(Exception err){
					    echo "Build failed: {err.message}"
					    currentBuild.result = 'FAILURE'
					    error(err)
				    }
                }
                
                
            }
        }

        stage('Test') {
            steps {
                script{
                     try{
                        bat "D:\\kpi-3\\5semester\\SystemProg\\lab4\\Skomoroha-Test\\x64\\Debug\\Skomoroha-Test.exe --gtest_output=xml:Skomoroha-Test.xml"
                     }
                     catch(Exception err){
                        echo "Test failed: {err.message}"
                        currentBuild.result = 'FAILURE'
                        error(err)
                    }
                }

               
            }
        }
    }

    post {
    always {
        // Publish test results using the junit step
         // Specify the path to the XML test result files
    }
}
}