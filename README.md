# android-signing-plugin
Gradle Android Signing Plugin

## Usage

Just apply plugin:
```groovy
apply plugin: 'android-signing'
```

Or with DSL:
```groovy
apply plugin: 'android-signing'

androidSignings {
   props "$projectDir/signing/dev.properties" 
   props "$projectDir/signing/release.properties" 
}

// Or
androidSignings {
   props "$projectDir/signing/" 
}

// Or
androidSignings {
   props "$projectDir/signing/*" 
}

// Or
androidSignings {
   props "$projectDir/signing/*.properties" 
}

// Or
androidSignings {
   props "$projectDir/signing/**/*.properties" 
}
```

Android config:
```groovy
apply plugin: 'com.android.application'
apply plugin: 'android-signing'

android {

    signingConfigs {
        dev
        release
    }

    buildTypes {
        release {
            signingConfig signingConfigs.release
            //...
        }
        debug {
            signingConfig signingConfigs.dev
            //...
        }
    }

    //...

}
```

_signing/dev.properties_
```properties
dev.storeFile=debug.keystore
dev.keyAlias=myapp
dev.storePassword=supersecure
dev.keyPassword=supersecure
```

_signing/release.properties_
```properties
release.storeFile=release.keystore
release.keyAlias=myapp
release.storePassword=${console}
release.keyPassword=${console}
```

_signing/release.properties_
```properties
release.storeFile=release.keystore
release.keyAlias=myapp
release.storePassword=${keychain}
release.keyPassword=${keychain}
```

_signing/release.properties_
```properties
release.storeFile=release.keystore
release.keyAlias=myapp
release.storePassword=${env(MY_APP_STORE_PASS)}
release.keyPassword=${env(MY_APP_KEY_PASS)}
```

## Lookup strategies

Default properties locations:
 - ~/.android-signings/*
 - ~/.gradle/*
 - $projectDir/*

Keystore locations:
 - $propertiesFileDir/*
 - ~/.android-signings/*
 - ~/.gradle/*
 - $projectDir/*
 