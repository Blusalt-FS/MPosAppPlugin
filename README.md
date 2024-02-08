# MPosAppPlugin

## Installation

## Step 1
```sh
#Create a github.properties file in the root folder of android. Path should be like below: E.g. "mySampleApp/android/github.properties"

# Add the following in github.properties:
USERNAME_GITHUB=MyUsernameOnGithub
TOKEN_GITHUB=TokenFromGithubClassicToken
```

## Step 2: build.gradle (project level)
Add the following to build.gradle(project level) file
```sh


buildscript {
    repositories {
      ...
    }
    dependencies {
      ...
    }
}

allprojects {
    def githubPropertiesFile = rootProject.file("github.properties")
    def githubProperties = new Properties()
    githubProperties.load(new FileInputStream(githubPropertiesFile))

    repositories {
        ...
                
        maven {
          url 'https://gitlab.com/api/v4/projects/4128550/packages/maven'
        }
        maven {
          name "GitHubPackages"
          url 'https://maven.pkg.github.com/Blusalt-FS/MPosAppPlugin'

          credentials {
            username githubProperties['USERNAME_GITHUB']
              password githubProperties['TOKEN_GITHUB']
            }
       }
    }
}

```


## Step 3: build.gradle (app)
All the following to build.gradle (app level)

```sh

dependencies{
  implementation 'net.blusalt:mposplugin:1.0'

#Incase you get an error, add the following below
  implementation 'com.dspread.print:dspread_print_sdk:1.2.0'
  implementation 'com.dspread.library:dspread_pos_sdk:4.3.8'
  
  implementation 'androidx.appcompat:appcompat:1.6.1'
  implementation 'com.google.android.material:material:1.9.0'
  implementation 'androidx.constraintlayout:constraintlayout:2.1.4'

  implementation 'com.github.davidmigloz:number-keyboard:3.1.0'
  implementation 'me.abhinay.input:currency-edittext:1.1'

  implementation 'pl.droidsonroids.gif:android-gif-drawable:1.2.25'

  def nav_version = "2.3.5"
  api "androidx.navigation:navigation-fragment:$nav_version"
  api "androidx.navigation:navigation-ui:$nav_version"

  api "androidx.navigation:navigation-dynamic-features-fragment:$nav_version"

  implementation 'com.google.code.gson:gson:2.8.9'

  api 'com.squareup.retrofit2:retrofit:2.9.0'
  api 'com.squareup.okhttp3:logging-interceptor:4.9.0'
  api 'com.squareup.retrofit2:converter-gson:2.9.0'
  api 'com.jakewharton.retrofit:retrofit2-kotlin-coroutines-adapter:0.9.2'
  implementation 'com.github.poovamraj:PinEditTextField:1.2.6'
}
```


## Usage

```kt




class MainActivity : AppActivityCompact {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main_pos)
        Pos.getINSTANCE().startMPOSplugin(this, "", object : TransactionCompletedCallBack {
            override fun onSuccess(terminalResponse: TerminalResponse?) {

            }

            override fun onFailure(statusCode: Int, errorObject: String?) {

            }


        })
    }
}
```

```java
class MainActivity extends AppActivityCompact {
    @override
    void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main_pos);

        Pos.getINSTANCE().startMPOSplugin(this, "", new TransactionCompletedCallBack() {
            @Override
            public void onSuccess(TerminalResponse terminalResponse) {

            }

            @Override
            public void onFailure(int statusCode, String errorObject) {

            }
        });
    }
}


