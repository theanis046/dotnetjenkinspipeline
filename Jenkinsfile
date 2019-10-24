// TODO add clean up of previous builds to save space on Jenkins
node {
        stage('Checkout') {
                checkout([
                    $class: 'GitSCM', 
                    branches: [[name: '*/master']], 
                    doGenerateSubmoduleConfigurations: false, 
                    extensions: [], 
                    submoduleCfg: [], 
                    userRemoteConfigs: [[url: 'https://github.com/theanis046/dotnetjenkinspipeline']]
                ])
        }
        stage('Build'){
            echo "Build phase Started!"
            
            sh """
            sudo rmdir .//build
            sudo mkdir build
            
            sudo dotnet publish -o ./build"""
            
            echo "build done"
            sh """sudo ls"""
            echo "Build phase ended!"
        }
        stage('zip'){
            echo "Zip Phase Started!"
            
            sh """
            sudo ls ./build/
            sudo zip .//build//app.zip -r .//build//"""
            
            echo "Zip phase ended!"
        }  
        
        stage('upload'){
           
            echo "Upload phase started!"

            sh """
            sudo ls
            aws s3 cp .//build//app.zip s3://anispipelinebucket
            """
            
            echo "Upload phase ended!"
        }  
}