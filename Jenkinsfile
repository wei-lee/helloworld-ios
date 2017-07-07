node('osx') {
    stage ('Checkout') {
        git url: 'https://github.com/wei-lee/helloworld-ios.git'
    }
    
    stage('Cocoapods') {
        sh 'pod install'
    }
    
    stage('Build') {
        xcodeBuild(
        cleanBeforeBuild: true,
        src: '.',
        schema: 'helloworld-ios-app',
        workspace: 'helloworld-ios-app',
        buildDir: 'build',
        bootstrapKeychain: true,
        sdk: 'iphoneos',
        exportMethod: 'ad-hoc',
        version: '0.1-apha',
        shortVersion: '0.1',
        bundleId: 'com.feedhenry.helloworld-ios-app',
        infoPlistPath: 'helloworld-ios-app/helloworld-ios-app-Info.plist',
        flags: '-fstack-protector -fstack-protector-all',
        teamId: 'GHPBX39444',
        teamName: 'Red Hat, Inc.',
        autoSign: false
    )
  }
  
  stage('CodeSign') {
      codeSign(
        profileId: params.BUILD_CREDENTIAL_ID,
        clean: true,
        bundleId: 'com.feedhenry.helloworld-ios-app',
        verify: true,
        ipaName: 'myapp',
        appPath: 'helloworld-ios/build/Release-iphoneos/helloworld-ios-app.app'
      )
  }
  
  stage('Archive') {
      archive 'helloworld-ios/build/Release-iphoneos/helloworld-ios-app.ipa'
  }
}