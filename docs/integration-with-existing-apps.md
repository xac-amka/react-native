---
id: integration-with-existing-apps
title: Бэлэн апптай нэгтгэх
---

<style>
  .toggler li {
    display: inline-block;
    position: relative;
    top: 1px;
    padding: 10px;
    margin: 0px 2px 0px 2px;
    border: 1px solid #05A5D1;
    border-bottom-color: transparent;
    border-radius: 3px 3px 0px 0px;
    color: #05A5D1;
    background-color: transparent;
    font-size: 0.99em;
    cursor: pointer;
  }
  .toggler li:first-child {
    margin-left: 0;
  }
  .toggler li:last-child {
    margin-right: 0;
  }
  .toggler ul {
    width: 100%;
    display: inline-block;
    list-style-type: none;
    margin: 0;
    border-bottom: 1px solid #05A5D1;
    cursor: default;
  }
  @media screen and (max-width: 960px) {
    .toggler li,
    .toggler li:first-child,
    .toggler li:last-child {
      display: block;
      border-bottom-color: #05A5D1;
      border-radius: 3px;
      margin: 2px 0px 2px 0px;
    }
    .toggler ul {
      border-bottom: 0;
    }
  }
  .toggler a {
    display: inline-block;
    padding: 10px 5px;
    margin: 2px;
    border: 1px solid #05A5D1;
    border-radius: 3px;
    text-decoration: none !important;
  }
  .display-language-objc .toggler .button-objc,
  .display-language-swift .toggler .button-swift,
  .display-language-android .toggler .button-android {
    background-color: #05A5D1;
    color: white;
  }
  block { display: none; }
  .display-language-objc .objc,
  .display-language-swift .swift,
  .display-language-android .android {
    display: block;
  }
</style>

Цоо шинээр гар утасны апп эхнээс нь хийх гэж байгаа бол React Native тун тохиромжтой. Гэсэн та мөн бэлэн натив аппликейшнд дан харагдац болон хэрэглэгчийн дамжлага зэргийг нэмэх зорилгоор бас ашиглаж болно. Цөөн хэдэн зүйл хийгээд л та React Native дээр суурилсан шинэ үйлдэл, нүүр, харагдацтай болох боломжтой. 

Ямар платформ дээр ашиглахаас хамаарах хийх арга нь өөр өөр байна.

<div class="toggler">
  <ul role="tablist" >
    <li id="objc" class="button-objc" aria-selected="false" role="tab" tabindex="0" aria-controls="objctab" onclick="displayTab('language', 'objc')">
      iOS (Objective-C)
    </li>
    <li id="swift" class="button-swift" aria-selected="false" role="tab" tabindex="0" aria-controls="swifttab" onclick="displayTab('language', 'swift')">
      iOS (Swift)
    </li>
    <li id="android" class="button-android" aria-selected="false" role="tab" tabindex="0" aria-controls="androidtab" onclick="displayTab('language', 'android')">
      Android (Java)
    </li>
  </ul>
</div>

<block class="objc swift android" />

## Гол агуулга

<block class="objc swift" />

React Native компонентуудыг iOS аппликейшндаа нэгтгэхэд хэрэгтэй алхам:

1. React Native хамаарах тохиргоо, чиглэлийн бүтцийг /directory structure/ хийх.
2. Аппдаа ашиглах React Native компонентууд нь ямар үүрэгтэйг ойлгох.
3. CocoaPods ашиглан эдгээр компонентуудаа dependencies гэж нэмэх.
4. JavaScript дотор React Native компонентуудаа хөгжүүлэх.
5. iOS апп дотроо `RCTRootView`-ыг нэмэх. Энэ нь React Native компонентууд чинь байрлах контейнер нь болох юм. 
6. React Native серверээ ажиллуулан, натив аппликейшнаа ажиллуулна.
7. Аппликейшны чинь React Native талаасаа хүссэнээр чинь ажиллаж байгаа эсэхийг нягтлах. 
<block class="android" />

React Native компонентуудыг Android аппликейшн руу нэгтгэхэд хэрэгтэй алхам:

1. React Native хамаарах тохиргоо, чиглэлийн бүтцийг хийх.
2. JavaScript дотор React Native компонентуудаа хөгжүүлэх.
3. Android апп дотроо `ReactRootView`-ыг нэмэх. Энэ нь React Native компонентууд чинь байрлах контейнер нь болох юм. 
4. React Native серверээ ажиллуулан, натив аппликейшнаа ажиллуулна.
5. Аппликейшны чинь React Native талаасаа хүссэнээр чинь ажиллаж байгаа эсэхийг нягтлах. 

<block class="objc swift android" />

## Урьдчилсан тохиргоо

<block class="objc swift" />

[Эхлэх зөвлөмж](getting-started.md)-өөс натив код ашиглан апп хэрхэн бүтээх тухай уншиж, iOS-т зориулсан React Native апп хийх хөгжүүлэлтийн орчныг хэрхэн бий болгох вэ гэдэгтээ танилцаарай. 

### 1. Чиглэлийн бүтцийг тохируулах

Эмх цэгцтэй ажиллахын тулд эхлээд React Native-ын нэгтгэсэн төсөлдөө зориулан шинээр фолдер үүсгэнэ. Тэгээд бэлэн байгаа iOS  төслөө `/ios` гэсэн дэд фолдерт хийнэ. 

<block class="android" />

[Эхлэх зөвлөмж](getting-started.md)-өөс натив код ашиглан апп хэрхэн бүтээх тухай уншиж, Android-д зориулсан React Native апп хийх хөгжүүлэлтийн орчныг хэрхэн бий болгох вэ гэдэгтээ танилцаарай. 

### 1. Чиглэлийн бүтцийг тохируулах

Эмх цэгцтэй ажиллахын тулд эхлээд React Native-ын нэгтгэсэн төсөлдөө зориулан шинээр фолдер үүсгэнэ. Тэгээд бэлэн байгаа Android  төслөө `/android`  гэсэн дэд фолдерт хийнэ. 

<block class="objc swift android" />

### 2. JavaScript dependencies суулгах

Төслийнхөө үндсэн чиглэл рүү очоод `package.json` гэсэн шинэ файл үүсгэнэ. Үүндээ доорх кодыг хуулна:

```
{
  "name": "MyReactNativeApp",
  "version": "0.0.1",
  "private": true,
  "scripts": {
    "start": "yarn react-native start"
  }
}
```

Дараа нь [yarn package manager суулгасан](https://yarnpkg.com/lang/en/docs/install/) байгаа эсэхийг шалгана.


`react` болон `react-native` пакэж суулгана. Терминал эсвэл command prompt-оо нээгээд `package.json` гэсэн файл бүхий хэсгийг олж ажиллуулна:

```
$ yarn add react-native
```

Ингэхэд доорхтой төстэй мессеж гарах учиртай (дээш нь гүйлгэж байж харна):

> warning "react-native@0.52.2" has unmet peer dependency "react@16.2.0".

Ийм бол зүгээр гэсэн үг ба бид одоо React-аа суулгах хэрэгтэй:

```
$ yarn add react@version_printed_above
```

Yarn нь шинээр `/node_modules` гэсэн фолдер үүсгэнэ. Энэхүү фолдер нь апп хийхэд чинь хэрэгтэй бүх Javascript dependencies-ыг хадгална. 

`.gitignore` файл дээрээ `node_modules/`-ыг нэмнэ. 

<block class="objc swift" />

### 3. CocoaPods суулгах

[CocoaPods](http://cocoapods.org) нь iOS болон macOS-ын хөгжүүлэлтэнд зориулсан пакэж менежмент хийх хэрэгсэл юм.
Бид үүнийг ашиглан одоогийн төсөл дээрээ жинхэнэ React Native framework кодыг нэмнэ. 
[Homebrew](http://brew.sh/) ашиглан CocoaPods суулгахыг танд санал болгож байна. 

```
$ brew install cocoapods
```

> CocoaPods-ыг ашиглахгүйгээр хийх нь техникийн хувьд боломжгүй бөгөөд ингэхийн тулд тусгай сан үүсгэж, холбоос бүхий нэмэлт ажил хийх ба энэ нь их төвөгтэй байх болно. 

<block class="objc swift" />

## React Native-ыг өөрийн аппдаа нэмэх 
<block class="objc" />

[Нэгтгэх апп](https://github.com/JoelMarcey/iOS-2048) нь [2048](https://en.wikipedia.org/wiki/2048_%28video_game%29) гэдэг тоглоом байлаа гэж бодъё.  React Native-гүйгээр натив аппликейшны гол зэс нь ингэж харагдана. 

<block class="swift" />

[Нэгтгэх апп](https://github.com/JoelMarcey/swift-2048) нь [2048](https://en.wikipedia.org/wiki/2048_%28video_game%29) гэдэг тоглоом байлаа гэж бодъё. React Native-гүйгээр натив аппликейшны гол цэс нь ингэж харагдана. 
<block class="objc swift" />

![Before RN Integration](/react-native/docs/assets/react-native-existing-app-integration-ios-before.png)

###  Xcode-д зориулсан Command Line tools 

Command Line Tools суулгана. Xcode цэс дэх "Preferences..." гэснийг сонгоно. Locations гэсэн панел дээр очин Command Line хэрэгслүүд гэсэн рүү ороод хамгийн сүүлийн хувилбаруудыг нь сонгон суулгана. 

![Xcode Command Line Tools](/react-native/docs/assets/GettingStartedXcodeCommandLineTools.png)

### CocoaPods dependencies-ыг тохируулах 

React Native-ыг аппликейшнтайгаа нэгтгэхийн өмнө та React Native framework-ын аль хэсгийг нь нэгтгэх вэ гэдгээ шийдэх хэрэгтэй. Бид CocoaPods ашиглан аль "subspecs"-ээс апп тань хамаарахыг тодорхойлно. 

Дэмждэг `subspec`-ын жагсаалтыг [`/node_modules/react-native/React.podspec`](https://github.com/facebook/react-native/blob/master/React.podspec) гэдгээс харна уу. Эдгээр нь ажиллагаанаас хамааран ерөнхийдөө нэр нь өгөгдсөн байгаа. Тухайлбал,`Core` `subspec` танд байнга хэрэг болох болно. Эндээс та `AppRegistry`, `StyleSheet`, `View`  болон React Native-ын бусад сан руу очих боломжтой. Хэрэв та React Native-ын  `Text` сан (жишээ нь `<Text>` элементүүд) нэмэхийг хүсвэл `RCTText` `subspec` хэрэг болно. Хэрэв та `Image` сан (жишээ нь `<Image>` элементүүд) нэмэхийг хүсвэл `RCTImage` `subspec` хэрэг болно. 

Та аппын аль `subspec` нь `Podfile` файлаас хамаарах вэ гэдгийг тодорхойлж өгөх боломжтой. `Podfile` файл үүсгэх хамгийн хялбар арга бол `/ios` дэд фолдер дахь CocoaPods `init` командыг ашиглах юм:

```
$ pod init
```

`Podfile` нь таны нэгтгэх ажилд туслах boilerplate буюу давтамж бүхий тохиргоог агуулдаг. Эцэстээ `Podfile` үүнтэй төстэй харагдана:

<block class="objc" />

```
# The target name is most likely the name of your project.
target 'NumberTileGame' do

  # Your 'node_modules' directory is probably in the root of your project,
  # but if not, adjust the `:path` accordingly
  pod 'React', :path => '../node_modules/react-native', :subspecs => [
    'Core',
    'CxxBridge', # Include this for RN >= 0.47
    'DevSupport', # Include this to enable In-App Devmenu if RN >= 0.43
    'RCTText',
    'RCTNetwork',
    'RCTWebSocket', # Needed for debugging
    'RCTAnimation', # Needed for FlatList and animations running on native UI thread
    # Add any other subspecs you want to use in your project
  ]
  # Explicitly include Yoga if you are using RN >= 0.42.0
  pod 'yoga', :path => '../node_modules/react-native/ReactCommon/yoga'

  # Third party deps podspec link
  pod 'DoubleConversion', :podspec => '../node_modules/react-native/third-party-podspecs/DoubleConversion.podspec'
  pod 'glog', :podspec => '../node_modules/react-native/third-party-podspecs/glog.podspec'
  pod 'Folly', :podspec => '../node_modules/react-native/third-party-podspecs/Folly.podspec'

end
```

<block class="swift" />

```
source 'https://github.com/CocoaPods/Specs.git'

# Required for Swift apps
platform :ios, '8.0'
use_frameworks!

# The target name is most likely the name of your project.
target 'swift-2048' do

  # Your 'node_modules' directory is probably in the root of your project,
  # but if not, adjust the `:path` accordingly
  pod 'React', :path => '../node_modules/react-native', :subspecs => [
    'Core',
    'CxxBridge', # Include this for RN >= 0.47
    'DevSupport', # Include this to enable In-App Devmenu if RN >= 0.43
    'RCTText',
    'RCTNetwork',
    'RCTWebSocket', # needed for debugging
    # Add any other subspecs you want to use in your project
  ]
  # Explicitly include Yoga if you are using RN >= 0.42.0
  pod "yoga", :path => "../node_modules/react-native/ReactCommon/yoga"

  # Third party deps podspec link
  pod 'DoubleConversion', :podspec => '../node_modules/react-native/third-party-podspecs/DoubleConversion.podspec'
  pod 'glog', :podspec => '../node_modules/react-native/third-party-podspecs/glog.podspec'
  pod 'Folly', :podspec => '../node_modules/react-native/third-party-podspecs/Folly.podspec'

end
```

<block class="objc swift" />

 `Podfile`-аа үүсгэсний дараа та React Native pod-ыг суулгахад бэлэн боллоо гэсэн үг.

```
$ pod install
```

Ийм үр дүн гарна:

```
Analyzing dependencies
Fetching podspec for `React` from `../node_modules/react-native`
Downloading dependencies
Installing React (0.26.0)
Generating Pods project
Integrating client project
Sending stats
Pod installation complete! There are 3 dependencies from the Podfile and 1 total pod installed.
```

> Хэрэв `xcrun` гэсэн алдаа заавал  Preferences > Locations доторх  Xcode-ын Command Line Tools нь өгөгдсөн эсэхийг шалгаарай. 

<block class="swift" />

> Хэрэв "_The `swift-2048 [Debug]`  гэхчлэн анхааруулга гарч ирвэл `Pods/Target Support Files/Pods-swift-2048/Pods-swift-2048.debug.xcconfig`-т тодорхойлсон `FRAMEWORK_SEARCH_PATHS` -ыг дарж ажиллана. Ингэснээр CocoaPods installation_" -д асуудал үүсэх тул  `Build Settings`  дахь `Framework Search Paths`  нь  `Debug` болон `Release`-т аль аль нь зөвхөн `$(inherited)` агуулсан байх хэрэгтэй.

<block class="objc swift" />

### Код нэгтгэх

Одоо бид натив iOS аппликейшны өөрчилж React Native-тай нийлүүлэх юм.  Жишээ болгон хийж буй 2048 апп хийхдээ бид React Native дээр "High Score" нүүрийг нэмж өгөх болно. 

#### React Native компонент

Бидний хамгийн эхэнд бичих код бол шинэ "High Score"-ыг дэлгэцэнд харуулах код ба үүнийгээ аппликейшндээ нэгтгэх хэрэгтэй. 


##### 1. `index.js` файл үүсгэх

Эхлээд React Native төсөлдөө  `index.js` гэсэн хоосон файл үүсгэнэ. 

`index.js` нь React Native аппликейшны эхлэх цэг нь байх бөгөөд үргэлж байх шаардлагатай. Жижиг файл React Native-ын компонент эсвэл аппликейшнд хамаарах бусад файлыг `require` шаардах эсвэл бүх хэрэгтэй кодыг өөртөө хадгалах боломжтой байна. Бидний хуьд бүгдийг нь `index.js` дотроо хийчихнэ.

##### 2. React Native кодоо нэмэх

`index.js` дотроо өөрийн компонентоо үүсгэнэ.  Бидний жишээ дээр `<Text>` компонентоо хэв маягийг тодорхойлсон `<View>` буюу харагдац дээрээ нэмнэ.

```javascript
import React from 'react';
import {AppRegistry, StyleSheet, Text, View} from 'react-native';

class RNHighScores extends React.Component {
  render() {
    var contents = this.props['scores'].map((score) => (
      <Text key={score.name}>
        {score.name}:{score.value}
        {'\n'}
      </Text>
    ));
    return (
      <View style={styles.container}>
        <Text style={styles.highScoresTitle}>2048 High Scores!</Text>
        <Text style={styles.scores}>{contents}</Text>
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#FFFFFF',
  },
  highScoresTitle: {
    fontSize: 20,
    textAlign: 'center',
    margin: 10,
  },
  scores: {
    textAlign: 'center',
    color: '#333333',
    marginBottom: 5,
  },
});

// Module name
AppRegistry.registerComponent('RNHighScores', () => RNHighScores);
```

> `RNHighScores` is the name of your module that will be used when you add a view to React Native from within your iOS application.

#### Ид шид: `RCTRootView`

`index.js` ашиглан React Native компонент үүссэн учир та одоо шинэ эсвэл хуучин `ViewController` дээрээ уг компонентоо нэмнэ. Хамгийн хялбар арга нь компонентдоо зориулсан эвент зам үүсгээд, тухайн компонентоо хуучин `ViewController` дээрээ нэмнэ. 

Бид React Native компонентоо `ViewController` дахь шинэ натив харагдацтай холбох ба үүнийг `RCTRootView` гэж нэрлэдэг. 


##### 1. Шинэ эвентийн зам үүсгэх

Та React Native хуудас дээрх "High Score" гэсэн дээрээс тоглоомын үндсэн цэс дээр шинэ холбоос нэмж болно. 

![Event Path](/react-native/docs/assets/react-native-add-react-native-integration-link.png)

##### 2. Эвент зохицуулагч

Одоо тэгээд цэсний холбоо дээрээс event handler-аа нэмнэ. Аппликейшны тань гол `ViewController` дээр нэмэгдэх болно. Ингэснээр `RCTRootView` нь ажиллана. 

React Native аппликейшн хийх үед та React Native пакэж ашиглан `index.bundle` үүсгэнэ. Энэ нь React Native-ын серверийг ашигладаг. `index.bundle`  дотор бидний `RNHighScore` модуль байна. Тийм болохоор `NSURL`-ыг ашиглан `RCTRootView`-т `index.bundle`-ын байрлалыг зааж өгч, модультай холбоно. 

Дибаг хийх зорилгоор дуудагдсан эвент зохицуулагчийг нь лог хийнэ. Тэгээд `index.bundle` дотор байх React Native кодын байрлал бүхий стринг бүтээнэ. Эцэст нь бид гол `RCTRootView`-ээ хийнэ. React Native компонентынхоо кодыг бичихдээ [дээр](#the-react-native-component) үүсгэсэн `moduleName` шигээ `RNHighScores`-ыг гаргаж өгч байгааг анзаарна уу. 


<block class="objc" />

Эхлээд `RCTRootView`-ыг `import` хийнэ.

```objectivec
#import <React/RCTRootView.h>
```

> `initialProperties` нь илүү тодорхой харуулах зорилготой ба өндөр онооны дэлгэцийн мэдээллийг авах боломжтой болно. 
 React Native компонентдоо бид `this.props` ашиглан энэхүү мэдээллийг авах боломжтой.  

```objectivec
- (IBAction)highScoreButtonPressed:(id)sender {
    NSLog(@"High Score Button Pressed");
    NSURL *jsCodeLocation = [NSURL URLWithString:@"http://localhost:8081/index.bundle?platform=ios"];

    RCTRootView *rootView =
      [[RCTRootView alloc] initWithBundleURL: jsCodeLocation
                                  moduleName: @"RNHighScores"
                           initialProperties:
                             @{
                               @"scores" : @[
                                 @{
                                   @"name" : @"Alex",
                                   @"value": @"42"
                                  },
                                 @{
                                   @"name" : @"Joel",
                                   @"value": @"10"
                                 }
                               ]
                             }
                               launchOptions: nil];
    UIViewController *vc = [[UIViewController alloc] init];
    vc.view = rootView;
    [self presentViewController:vc animated:YES completion:nil];
}
```

> `RCTRootView initWithURL` нь шинэ JSC VM үүсгэж буйг анзаарна уу. Натив аппынхаа өөр өөр хэсэг дахь RN хоорондох харилцааг илүү энгийн болгож, хадгалахын тулд та нэг удаад JS ажиллах  React Native-ын олон харагдацтай байх функцыг ашиглаж боломжтой. 
Үүний тулд `[RCTRootView alloc] initWithURL`-ыг биш, [`RCTBridge initWithBundleURL`](https://github.com/facebook/react-native/blob/master/React/Base/RCTBridge.h#L93) ашиглан bridge үүсгээд  `RCTRootView initWithBridge` ашиглаарай. 

<block class="swift" />

Эхлээд `React` сангаа `import`хийнэ.

```javascript
import React
```

> `initialProperties` нь илүү тодорхой харуулах зорилготой ба өндөр онооны дэлгэцийн мэдээллийг бид авах боломжтой болно. 
 React Native компонентдоо бид `this.props` ашиглан энэхүү мэдээллийг авах боломжтой.  
 

```swift
@IBAction func highScoreButtonTapped(sender : UIButton) {
  NSLog("Hello")
  let jsCodeLocation = URL(string: "http://localhost:8081/index.bundle?platform=ios")
  let mockData:NSDictionary = ["scores":
      [
          ["name":"Alex", "value":"42"],
          ["name":"Joel", "value":"10"]
      ]
  ]

  let rootView = RCTRootView(
      bundleURL: jsCodeLocation,
      moduleName: "RNHighScores",
      initialProperties: mockData as [NSObject : AnyObject],
      launchOptions: nil
  )
  let vc = UIViewController()
  vc.view = rootView
  self.present(vc, animated: true, completion: nil)
}
```

> `RCTRootView bundleURL` нь шинэ JSC VM үүсгэж буйг анзаарна уу. Натив аппынхаа өөр өөр хэсэг дэх RN хоорондох харилцааг илүү энгийн болгож, хадгалахын тулд та нэг удаад JS ажиллах React Native-ын олон харагдацтай байх функцыг ашиглаж боломжтой. 
Үүний тулд `RCTRootView bundleURL`-ны оронд [`RCTBridge initWithBundleURL`](https://github.com/facebook/react-native/blob/master/React/Base/RCTBridge.h#L89) ашиглан bridge үүсгээд, `RCTRootView initWithBridge` ашиглаарай. 

<block class="objc" />

> Аппаа боловсруулж бэлэн болох үед `NSURL` нь `[[NSBundle mainBundle] URLForResource:@"main" withExtension:@"jsbundle"];` -тай төстэй зүйлийг ашиглан диск дээрх урьдаар bundle хийсэн файлыг зааж өгөх болно. Та `node_modules/react-native/scripts/` доторх  `react-native-xcode.sh`-ыг ашиглан урьдаар bundle хийсэн файлаа гаргана.

<block class="swift" />

> Аппаа боловсруулж бэлэн болох үед `NSURL` нь `let mainBundle = NSBundle(URLForResource: "main" withExtension:"jsbundle")` -тай төстэй зүйлийг ашиглан диск дээрх урьдаар bundle хийсэн файлыг зааж өгөх болно. Та `node_modules/react-native/scripts/` доторх  `react-native-xcode.sh`-ыг ашиглан урьдаар bundle хийсэн файлаа гаргана.

<block class="objc swift" />

##### 3. Холбох 

 Үндсэн цэс дэх шин холбоосыг шинээр нэмсэн эвент зохицуулагчтай холбоно.

![Event Path](/react-native/docs/assets/react-native-add-react-native-integration-wire-up.png)

> Үүнийг хийх нэг хялбар арга нь storyboard дээрээ харагдацыг нээн, шинэ холбоос дээр маус 2-оо дарна. `Touch Up Inside`-ыг даран  storyboard руу чирээд байгаа жагсаалтнаас сонголтоо хийнэ.

### Нэгтгэсэн үйлдлээ тест хийх

Та React Native-ыг бэлэн аппликейшнтэйгээ холбох үндсэн алхмуудыг хийж дууслаа. Одоо бид React Native packager ажиллуулан `index.bundle` пакэжийг үүсгээд `localhost` ажиллуулах серверээ хийнэ. 

##### 1. Апп шилжүүлэх аюулгүй байдлын өргөтгөлийг нэмэх 


Apple далд хэлбэрийн энгийн HTTP ачаалахыг хориглосон байдаг. Тиймээс бид `Info.plist` эсвэл үүнтэй ижил файлыг нэмж өгөх хэрэгтэй.


```xml
<key>NSAppTransportSecurity</key>
<dict>
    <key>NSExceptionDomains</key>
    <dict>
        <key>localhost</key>
        <dict>
            <key>NSTemporaryExceptionAllowsInsecureHTTPLoads</key>
            <true/>
        </dict>
    </dict>
</dict>
```

> Апп шилжүүлэх аюулгүй байдлын функц нь хэрэглэгчдэд тустай. Аппаа бэлэн болгож гаргахаасаа өмнө дахин идэвхжүүлэхээ мартаж болохгүй. 


##### 2. Packager ажиллуулах

Аппаа ажиллуулахын тулд та эхлээд хөгжүүлэлтийн серверээ эхлүүлэх хэрэгтэй. Ингэхийн тул React Native төслийнхөө root directory  дотор доорх командыг өгнө:

```
$ npm start
```

##### 3. Апп ажиллуулах

Хэрэв та Xcode юм уу эсвэл өөрийн дуртай нэг засагчийг ашиглаж байгаа бол натив iOS аппликейшнаа энгийн ажиллуулдаг шигээ ажиллуулж хийнэ. Өөрөөр та доорх командыг ашиглан аппаа ажиллуулах боломжтой:

```
# From the root of your project
$ react-native run-ios
```

Жишээ болгож хийсэн аппликейшн дээр та "High Scores"-ыг заасан холбоос байгаа. Та дээр нь дарахад React Native компонент рендэр хийнэ. 

 _native_ application дэлгэц:

![Home Screen](/react-native/docs/assets/react-native-add-react-native-integration-example-home-screen.png)

_React Native_ өндөр онооны дэлгэц:

![High Scores](/react-native/docs/assets/react-native-add-react-native-integration-example-high-scores.png)

> Хэрэв таныг аппликейшнээ ажиллуулж байхад модультай холбоотой асуудал үүсвэл [GitHub](https://github.com/facebook/react-native/issues/4968) дээр хэрхэн шийдсэн болохыг нь уншаарай.  [Энэ хариулт](https://github.com/facebook/react-native/issues/4968#issuecomment-220941717) дээр хамгийн сүүлийн үеийн боломжит шийдлийг бичсэн байна.

### Кодоо харах

<block class="objc" />

Жишээ болгон хийсэн аппынхаа React Native  дэлгэц дээр хийсэн кодоо [GitHub](https://github.com/JoelMarcey/iOS-2048/commit/9ae70c7cdd53eb59f5f7c7daab382b0300ed3585) дээрээс та харж болно. 

<block class="swift" />

Жишээ болгон хийсэн аппынхаа React Native  дэлгэц дээр хийсэн кодоо [GitHub](https://github.com/JoelMarcey/swift-2048/commit/13272a31ee6dd46dc68b1dcf4eaf16c1a10f5229) дээрээс та харж болно. 

<block class="android" />

## Апп дээрээ React Native нэмэх 

### Maven тохиргоо хийх

React Native dependency-ыг аппынхаа `build.gradle` файл дээр нэм:

```gradle
dependencies {
    implementation 'com.android.support:appcompat-v7:27.1.1'
    ...
    implementation "com.facebook.react:react-native:+" // From node_modules
}
```

> Хэрэв та үргэлж React Native-ын нэг хувилбарыг ашиглахыг хүсвэл `+` тэмдгийг `npm`-ээс татсан React Native  хувилбараараа орлуулаарай. 

React Native maven directory-даа `build.gradle`-ыг нэмнэ. Ингэхдээ бусдын дээр нь байх "allprojects" блок дээрээ нэмээрэй:

```gradle
allprojects {
    repositories {
        maven {
            // All of React Native (JS, Android binaries) is installed from npm
            url "$rootDir/../node_modules/react-native/android"
        }
        ...
    }
    ...
}
```

> Замаа зөв зааж өгсөн эсэхээ шалгаарай! Android Studio дээр Gradle sync ажиллуулахад “Failed to resolve: com.facebook.react:react-native:0.x.x" гэх мэт алдаа гарах учиргүй.

### Зөвшөөрлийн тохиргоо хийх

Дараа нь `AndroidManifest.xml` дотор интернэт зөвшөөрөл байгаа эсэхийг шалгаарай:

    <uses-permission android:name="android.permission.INTERNET" />

Хэрэв та `DevSettingsActivity`-руу холбогдох хэрэгтэй бол `AndroidManifest.xml` дээрээ нэмээрэй:

    <activity android:name="com.facebook.react.devsupport.DevSettingsActivity" />

Хөгжүүлэлтийн серверээс JavaScript дахин ачаалах үед хөгжүүлэлтийн горимд байгаа үед ашиглах боломжтой. Тийм болохоор та хэрэгтэй үедээ бэлэн болсон үед нь хандаж болно.

### Cleartext Traffic (API level 28+)

> Android 9 (API level 28)-аас хойш хувилбарт цаанаасаа кодлогдоогүй мэдээлэл солилцох боломжийг хаасан байдаг. Энэ нь таны аппликейшныг the React Native packager-тай холбогдоход саад болдог.  Дибагийн үед кодлоогүй мэдээллийг хэрхэн нэвтрүүлэх тухай доороос уншина уу. 

#### 1. `AndroidManifest.xml`-тээ `usesCleartextTraffic` сонголтыг нэмэх 

```xml
<!-- ... -->
<application
  android:usesCleartextTraffic="true" tools:targetApi="28" >
  <!-- ... -->
</application>
<!-- ... -->
```
Апп бэлэн болж, гаргахад энэ нь заавал байх шаардлагагүй.

Сүлжээний аюулгүй байдлыг тохиргоо болон кодлоогүй мэдээллийн тухай дэлгэрэнгүй мэдэхийг хүсвэл [энэ холбоос](https://developer.android.com/training/articles/security-config#CleartextTrafficPermitted) руу орно уу.

### Кодоо нэгтгэх

Одоо бид натив Android аппликейшнаа React Native-тай нэгтгэнэ. 

#### React Native компонент

Эхлээд бид аппликейшнтайгаа нэгтгэх "High Score" нүүрээ бичих React Native кодоо бичих хэрэгтэй. 

##### 1. `index.js` файл үүсгэ.

Эхлээд React Native төслийн голд хоосон `index.js` файл үүсгэнэ. 

React Native  аппликейшн хийх үед `index.js`-ээс эхлэх ба байнга байх шаардлагатай. React Native компонент эсвэл аппликейшны чинь хэрэг болсон өөр бусад файлыг `require` хийх жижиг файл байж болно. Эсвэл шаардлагатай бүх кодыг агуулсан байж болно. Бидний хувьд бүгдийг нь `index.js` дотроо хийнэ.

##### 2. React Native кодоо нэмэх

`index.js` дотроо өөрийн компонентоо үүсгэнэ.  Бидний жишээ дээр бол энгийн `<Text>` компонентыг `<View>` дээр хэв маягийг тодорхойлон хийнэ гэсэн үг:

```javascript
import React from 'react';
import {AppRegistry, StyleSheet, Text, View} from 'react-native';

class HelloWorld extends React.Component {
  render() {
    return (
      <View style={styles.container}>
        <Text style={styles.hello}>Hello, World</Text>
      </View>
    );
  }
}
var styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
  },
  hello: {
    fontSize: 20,
    textAlign: 'center',
    margin: 10,
  },
});

AppRegistry.registerComponent('MyReactNativeApp', () => HelloWorld);
```

##### 3. Хөгжүүлэлтийн алдаа давхцахад зориулсан зөвшөөрөл өгөх процессын тохиргоо хийх

Хэрэв та аппаа Android `API level 23` юм уу түүнээс дээш хувилбарт зориулж хийж байгаа бол хөгжүүлэлтийн тохиргоондоо `android.permission.SYSTEM_ALERT_WINDOW`-ыг идэвхжүүлсэн эсэхээ шалгаарай. Та `Settings.canDrawOverlays(this);`-ыг ашиглан шалгах боломжтой. React Native хөгжүүлэлтийн алдаа нь бусад бүх цонхны дээр харагдах учир үүнийг хөгжүүлэлтийн горимд байхад нь шалгах хэрэгтэй. API level 23 (Android M) дээр зөвшөөрлийн шинэ системтэй болсон тул хэрэглэгч үүнийг баталгаажуулах хэрэгтэй болсон. Үүний тулд доорх кодыг `onCreate()` дахь Activity гэсэн дээр нэмэхэд болно. 

```java
private final int OVERLAY_PERMISSION_REQ_CODE = 1;  // Choose any value

...

if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.M) {
    if (!Settings.canDrawOverlays(this)) {
        Intent intent = new Intent(Settings.ACTION_MANAGE_OVERLAY_PERMISSION,
                                   Uri.parse("package:" + getPackageName()));
        startActivityForResult(intent, OVERLAY_PERMISSION_REQ_CODE);
    }
}
```

Эцэст нь UX буюу хэрэглэгчийн ашиглалтад нийцүүлэн зөвшөөрөл Хүлээн зөвшөөрсөн эсвэл Няцаасан тохиолдолд `onActivityResult()` (доор кодыг нь харуулсан) дарагдаж бичигдэнэ. Бид гарсан дүнг `ReactInstanceManager`-ынхаа `onActivityResult`-д дамжуулах хэрэгтэй. 

```java
@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    if (requestCode == OVERLAY_PERMISSION_REQ_CODE) {
        if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.M) {
            if (!Settings.canDrawOverlays(this)) {
                // SYSTEM_ALERT_WINDOW permission not granted
            }
        }
    }
    mReactInstanceManager.onActivityResult( this, requestCode, resultCode, data );
}
```

#### Ид шид: `ReactRootView`

 React Native ажиллах хугацааг эхлүүлэхийн тул бид натив код нэмэх хэрэгтэй бөгөөд JS компонентыг рендэр хийх даалгавар өгнө. Ингэхийн тулд бид дотроо React аппликейшныг ажиллуулж, гол харагдац болгодог `ReactRootView` үүсгэх `Activity` гаргана.. 


> Хэрэв та  Android <5 хувилбарт зориулж хийж байгаа бол `Activity`-ын оронд `com.android.support:appcompat`  пакэжийн `AppCompatActivity` классийг ашиглаарай. 

```java
public class MyReactActivity extends Activity implements DefaultHardwareBackBtnHandler {
    private ReactRootView mReactRootView;
    private ReactInstanceManager mReactInstanceManager;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        mReactRootView = new ReactRootView(this);
        mReactInstanceManager = ReactInstanceManager.builder()
                .setApplication(getApplication())
                .setCurrentActivity(this)
                .setBundleAssetName("index.android.bundle")
                .setJSMainModulePath("index")
                .addPackage(new MainReactPackage())
                .setUseDeveloperSupport(BuildConfig.DEBUG)
                .setInitialLifecycleState(LifecycleState.RESUMED)
                .build();
        // The string here (e.g. "MyReactNativeApp") has to match
        // the string in AppRegistry.registerComponent() in index.js
        mReactRootView.startReactApplication(mReactInstanceManager, "MyReactNativeApp", null);

        setContentView(mReactRootView);
    }

    @Override
    public void invokeDefaultOnBackPressed() {
        super.onBackPressed();
    }
}
```

> Хэрэв та React Native-т зориулсан анхлан суралцагчдад зориулсан багцыг ашиглаж байгаа бол "HelloWorld"  стрингийг index.js  файл доторх нэгээр солиорой (`AppRegistry.registerComponent()` аргын нэг аргумент нь энэ).

Хэрэв та Android Studio ашиглаж байгаа бол `Alt + Enter` ашиглан MyReactActivity класс дотроо дутуу байгаа бүх импортуудаа нэмээрэй. Пакэжийнхаа `BuildConfig`-ыг ашиглахдаа болгоомжтой хандаарай. `facebook` пакэжныг ашиглаж болохгүй. 

Хэрэглэгчийн интерфэйсийн зарим компонентууд нь энэ theme-ээс хамаарах тул `Theme.AppCompat.Light.NoActionBar` дээр `MyReactActivity`-ын theme-ыг тохируулж өгөх шаардлагатай. 


```xml
<activity
  android:name=".MyReactActivity"
  android:label="@string/app_name"
  android:theme="@style/Theme.AppCompat.Light.NoActionBar">
</activity>
```

> `ReactInstanceManager`-ыг олон үйлдэл, хэсэг ашиглаж болно. Та өөрийн `ReactFragment` эсвэл `ReactActivity` үүсгэн `ReactInstanceManager`-ыг агуулах дан _holder_ эзэмших болно. `ReactInstanceManager` хэрэгтэй үед 
(жишээлбэл, `ReactInstanceManager`-ыг тэдгээр үйлдэл, хэсгийн мөчлөгт холбох) энэ ганцыгаа ашиглах боломжтой. 

Дараа нь бид `ReactInstanceManager` болон `ReactRootView`-т зарим үйлдлийн мөчлөгийг эргэн дуудан дамжуулах хэрэгтэй:

```java
@Override
protected void onPause() {
    super.onPause();

    if (mReactInstanceManager != null) {
        mReactInstanceManager.onHostPause(this);
    }
}

@Override
protected void onResume() {
    super.onResume();

    if (mReactInstanceManager != null) {
        mReactInstanceManager.onHostResume(this, this);
    }
}

@Override
protected void onDestroy() {
    super.onDestroy();

    if (mReactInstanceManager != null) {
        mReactInstanceManager.onHostDestroy(this);
    }
    if (mReactRootView != null) {
        mReactRootView.unmountReactApplication();
    }
}
```
Бид мөн буцах товчлуурын эвентийг React Native-т дамжуулна:

```java
@Override
 public void onBackPressed() {
    if (mReactInstanceManager != null) {
        mReactInstanceManager.onBackPressed();
    } else {
        super.onBackPressed();
    }
}
```
Энэ нь хэрэглэгч буцах товчийг дарах үед JavaScript-ыг удирдах зорилготой (жишээ нь навигаци хийх).  JavaScript буцаах товч дарах үйлдлийг зохицуулахгүй бол  `invokeDefaultOnBackPressed` аргыг дуудна. Цаанаасаа уг функц нь таны `Activity`-ыг дуусгавар болгоно.

Эцэст нь бид хөгжүүлэгчийн цэсийг холбох хэрэгтэй. Төхөөрөмжийг сэгсрэх үед идэвхжүүлэх тохиргоо цаанаас хийгдсэн байдаг ч эмуляторт бол энэ нь төдийлөн үр дүнтэй байж чаддаггүй. Цэсний товчийг дарах үед юу болохыг харуулдаг( Android Studio эмулятор ашиглаж байгаа бол `Ctrl + M` дар):

```java
@Override
public boolean onKeyUp(int keyCode, KeyEvent event) {
    if (keyCode == KeyEvent.KEYCODE_MENU && mReactInstanceManager != null) {
        mReactInstanceManager.showDevOptionsDialog();
        return true;
    }
    return super.onKeyUp(keyCode, event);
}
```
Одоо таны үйлдэл Javascript кодтой ажиллахад бэлэн боллоо. 

### Нэгтгэсэн эсэхээ шалгах

Бид React Native-ыг бэлэн аппликейшнтай холбох үндсэн алхмуудыг мэддэг боллоо. Одоо бид React Native packager ашиглан `index.bundle` пакэж болон ажиллуулах серверийг үүсгэнэ.

##### 1. Packager ажиллуулах 

Аппаа ажиллуулахын тулд та эхлээд хөгжүүлэгчийн серверээ ажиллуулах хэрэгтэй. Ингэхийн тулд React Native төслийнхөө голд доорх командыг өгнө:

```
$ yarn start
```

##### 2. Аппаа ажиллуулах

Одоо Android аппаа зүгээр л энгийн үед ажиллуулдаг шигээ ажилуулна. 

Апп дотор  React-ын нөлөөтэй үйлдэлд хүрэх үед хөгжүүлэгчийн серверээс JavaScript код ачаалж, харуулна:

![Screenshot](/react-native/docs/assets/EmbeddedAppAndroid.png)

### Android Studio дотор бэлэн загвараа үүсгэх

Та Android Studio ашиглан бэлэн загвараа үүсгэх боломжтой! Өмнөх натив Android апптай чинь адил бэлэн загварыг гаргахад хялбар байх болно. Ердөө ганцхан нэмэлт алхам бий. Үүнийг бэлэн загвараа гаргахаас өмнө хийх хэрэгтэй. Та доорх ажиллуулж, React Native bundle үүсгэнэ. Энэ нь натив Android апп дотор агуулагдана:

```
$ react-native bundle --platform android --dev false --entry-file index.js --bundle-output android/com/your-company-name/app-package-name/src/main/assets/index.android.bundle --assets-dest android/com/your-company-name/app-package-name/src/main/res/
```

> Замыг заахдаа зөвийг нь сонгож,  assets folder байхгүй бол нээгээрэй.

Одоо харин Android Studio-д натив апп хийдэг шигээ л бэлэн загвараа гаргана. Тэгээд л боллоо!

<block class="objc swift android" />

### Одоо яах уу?

Одоо та аппаа үргэлжлүүлэн хөгжүүлж болно. [debugging](debugging.md) болон [deployment](running-on-device.md) гэсэн хэсгээс   React Native-т хэрхэн ажиллах тухай дэлгэрэнгүй уншаарай.

<script>
  function displayTab(type, value) {
    var container = document.getElementsByTagName('block')[0].parentNode;
    container.className = 'display-' + type + '-' + value + ' ' +
      container.className.replace(RegExp('display-' + type + '-[a-z]+ ?'), '');
  }
  function convertBlocks() {
    // Convert <div>...<span><block /></span>...</div>
    // Into <div>...<block />...</div>
    var blocks = document.querySelectorAll('block');
    for (var i = 0; i < blocks.length; ++i) {
      var block = blocks[i];
      var span = blocks[i].parentNode;
      var container = span.parentNode;
      container.insertBefore(block, span);
      container.removeChild(span);
    }
    // Convert <div>...<block />content<block />...</div>
    // Into <div>...<block>content</block><block />...</div>
    blocks = document.querySelectorAll('block');
    for (var i = 0; i < blocks.length; ++i) {
      var block = blocks[i];
      while (
        block.nextSibling &&
        block.nextSibling.tagName !== 'BLOCK'
      ) {
        block.appendChild(block.nextSibling);
      }
    }
  }
  function guessPlatformAndOS() {
    if (!document.querySelector('block')) {
      return;
    }
    // If we are coming to the page with a hash in it (i.e. from a search, for example), try to get
    // us as close as possible to the correct platform and dev os using the hashtag and block walk up.
    var foundHash = false;
    if (
      window.location.hash !== '' &&
      window.location.hash !== 'content'
    ) {
      // content is default
      var hashLinks = document.querySelectorAll(
        'a.hash-link'
      );
      for (
        var i = 0;
        i < hashLinks.length && !foundHash;
        ++i
      ) {
        if (hashLinks[i].hash === window.location.hash) {
          var parent = hashLinks[i].parentElement;
          while (parent) {
            if (parent.tagName === 'BLOCK') {
              // Could be more than one target os and dev platform, but just choose some sort of order
              // of priority here.
              // Dev OS
              if (parent.className.indexOf('mac') > -1) {
                displayTab('os', 'mac');
                foundHash = true;
              } else if (
                parent.className.indexOf('linux') > -1
              ) {
                displayTab('os', 'linux');
                foundHash = true;
              } else if (
                parent.className.indexOf('windows') > -1
              ) {
                displayTab('os', 'windows');
                foundHash = true;
              } else {
                break;
              }
              // Target Platform
              if (parent.className.indexOf('ios') > -1) {
                displayTab('platform', 'ios');
                foundHash = true;
              } else if (
                parent.className.indexOf('android') > -1
              ) {
                displayTab('platform', 'android');
                foundHash = true;
              } else {
                break;
              }
              // Guide
              if (parent.className.indexOf('native') > -1) {
                displayTab('guide', 'native');
                foundHash = true;
              } else if (
                parent.className.indexOf('quickstart') > -1
              ) {
                displayTab('guide', 'quickstart');
                foundHash = true;
              } else {
                break;
              }
              break;
            }
            parent = parent.parentElement;
          }
        }
      }
    }
    // Do the default if there is no matching hash
    if (!foundHash) {
      var isMac = navigator.platform === 'MacIntel';
      var isWindows = navigator.platform === 'Win32';
      displayTab('platform', isMac ? 'ios' : 'android');
      displayTab(
        'os',
        isMac ? 'mac' : isWindows ? 'windows' : 'linux'
      );
      displayTab('guide', 'quickstart');
      displayTab('language', 'objc');
    }
  }
  convertBlocks();
  guessPlatformAndOS();
</script>
