# io-react-native-talk

## Build tools / Dependency management
#### [yarn](https://yarnpkg.com/en/) (or npm)
#### [Babel](https://babeljs.io/)

#### [React Native Packager](https://github.com/facebook/react-native/blob/master/packager/README.md)

#### [Gradle](https://gradle.org/)
Java build system used for android
* Configurations for 
* Release builds must be signed
* Proguard obfiscates bytecode and complains a lot
* Useful to get variables from JS files at build-time
```groovy
import groovy.json.JsonSlurper
def packageSlurper = new JsonSlurper()
def packageJson = packageSlurper.parse file('../../package.json')
println "Building Lifekeyrn v"+packageJson.version
// ......
defaultConfig {
    applicationId "com.lifekeyrn"
    minSdkVersion 16
    targetSdkVersion 22
    versionCode 1
    versionName packageJson.version
    ndk {
        abiFilters "armeabi-v7a", "x86"
    }
}
```
* You will have to spend some time with gradle to get native dependencies working
[Xcode]

## Libraries and SDKs
#### ES

#### Android
[Android React Native Bridge]()
### iOS

[Facebook React](https://facebook.github.io/react)
## Languages
[ECMAScript 2016 (ES7) with JSX](https://www.ecma-international.org/ecma-262/7.0/)
* fat-arrows, class syntax, import, static keyword, spread operator and more
* Babel transpiles it into ES3 which is what is run in the execution environment
* JSX (syntactic sugar for React.createElement) can be written inside ES7
```es6
function getGreeting(user) {
  if (user) {
    return <Text>Hello, {formatName(user)}!</Text>
  }
  return <Text>Hello, Stranger.</Text>;
}
```
* limited ES7 allowed inside JSX using {} 
```js
// POSSIBLE
render() {
  return (
    { this.state.ready ?
      <Text>Ready</Text>
      :
      <Text>Not Ready</Text>
    }
  )
}
// POSSIBLE
render() {
  if (this.state.ready) {
    return (<Text>Ready</Text>)
  } else {
    return (<Text>Not Ready</Text>)
  }
}
// IMPOSSIBLE
render() {
  return (
    { if (this.state.ready) {
      <Text>Ready</Text>
      } else {
      <Text>Not Ready</Text>
      }
    }
  )
}
```
* must be a valid expression. e.g if statements cannot be used because they compile to an invalid expression
```js
// VALID
const element = (
  <Text>
    Hello, world!
  </Text>
)

// ---->
const element = React.createElement(
  'Text',
  'Hello, world!'
)
// INVALID
const element = (
  if (this.state.worldExists) {
    <Text>
      Hello, world!
    </Text>
  } else {
    <Text>...</Text>
  }
)

// ---->
!!#*?##!???*#@##?????
```
#### [Facebook flow](https://flowtype.org/)

#### [Java](https://www.java.com/en/)
* It's just java

#### [Objective-C](https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/ProgrammingWithObjectiveC/Introduction/Introduction.html)
* Created in 1984
* Superset of C
* licensed by NeXT in 1988 who added support for it to gcc
* can be compiled with llvm, gcc or clang (but Xcode will handle that)
* wacky syntax
C
```c
// method call
myNiceOrange = newColor( 1.0, 0.6, 0.1, 1.0 );

// nested method calls
thing = inner.thing.secondThing.thirdThing.lastThing;
```
Objective-C
```objective-c
// method call
myNiceOrange = [NSColor colorWithRed:1.0 green:0.6 blue:0.1 alpha:1.0];

// nested method calls
thing = [[[[inner thing] secondThing] thirdThing] lastThing];
```
#### [Swift](https://swift.org/)
* Developed by Apple
* Released in June 2014
* inferred strong typing
* Intended to be more resilient to erroneous code ("safer") than Objective-C, and more concise
* Open Source [Github](https://github.com/apple/swift)
* Written in C++ (0_o ??)
``` objective-c
NSString *str = @"hello,";
str = [str stringByAppendingString:@" world"];
```
``` swift
var str = "hello,"
str += " world"
```
#### [Groovy](http://groovy-lang.org/)
* Used for gradle build scripts
* Simple syntax, easy to modify
* Knowledge not essential but helpful

## Environments

#### [JavaScriptCore](https://developer.apple.com/reference/javascriptcore)
On iOS and Android, hardware and simulator the bundle is executed on JavaScriptCore.
#### [V8](https://developers.google.com/v8/)
When debugging through chrome (I no recommend), the javascript will be executed on V8.

#### [Android API](https://developer.android.com/guide/index.html)
*[JRE](http://www.oracle.com/technetwork/java/javase/documentation/index.html)
*[Comparison of Java and Android API](https://en.wikipedia.org/wiki/Comparison_of_Java_and_Android_API)

#### [iOS](https://developer.apple.com/library/content/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/Introduction/Introduction.html#//apple_ref/doc/uid/TP40007072)
* Build setup using Xcode through GUI
* Native code written in Objective-C / Swift
