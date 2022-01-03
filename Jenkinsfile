pipeline {
  agent any
  environment {
    APPSYSID = '238880921b6881101c7a415de54bcbc7'
    CREDENTIALS = 'servicenow'
    DEVENV = 'https://hclnowintelligence.service-now.com'
    TESTENV = 'https://hcltechdemosls4.service-now.com'
    TESTSUITEID = 'bf8c266d732333005ce769972bf6a777'
  }
    

stages {
    stage('Build') {
      steps {
        snApplyChanges(appSysId: "${APPSYSID}", url: "${DEVENV}", credentialsId: "${CREDENTIALS}")
        snPublishApp(credentialsId: "${CREDENTIALS}", url: "${DEVENV}", appSysId: "${APPSYSID}",
          isAppCustomization: true, obtainVersionAutomatically: true, incrementBy: 2)
        
       
        
      }
    }
    
    
    stage('Install'){
           steps {
        snDevOpsChange()
        snInstallApp(credentialsId: "${CREDENTIALS}", url: "${TESTENV}", appSysId: "${APPSYSID}", baseAppAutoUpgrade: false)
        snRunTestSuite(credentialsId: "${CREDENTIALS}", url: "${TESTENV}", testSuiteSysId: "${TESTSUITEID}", withResults: true)
        
      }
    }


}

}
