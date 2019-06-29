---
id: troubleshooting
title: Алдаа олох
---

React Native-ын тохиргоог хийх үед түгээмэл тохиолддог асуудлууд байдаг. Хэрэв танд доорх жагсаалтанд багтаагүй ямар нэг асуудал тохиолдвол [GitHub дээр тухайн асуудлаа хайгаад үзээрэй](https://github.com/facebook/react-native/issues/).

### Портыг аль хэдийн ашиглаж байна

React Native нь 8081 порт дээр ажилладаг. Хэрэв өөр нэг нь уг портыг ашиглаж байвал та зогсоох эсвэл портоо солих арга хэмжээ авч болно. 

#### Порт 8081-г ашиглаж байгааг болиулах 

Порт 8081-г ашиглаж байгаа үйлдлийн id-ыг олохын тулд доорх командыг өгнө:

```
$ sudo lsof -i :8081
```
Тэгээд  доорхыг ашиглан уг процессыг зогсооно:

```
$ kill -9 <PID>
```

Windows дээр та [Resource Monitor](https://stackoverflow.com/questions/48198/how-can-you-find-out-which-process-is-listening-on-a-port-on-windows) ашиглан порт 8081 дээр үйлдлийг олох боломжтой ба Task Manager ашиглан зогсоож болно. 

#### 8081-ээс өөр порт ашиглах

Та 8081-ээс өөр порт ашиглахдаа `port` параметр ашиглана:

```
$ react-native start --port=8088
```

Шинээр сонгосон портноосоо Javascript багцаа ачаалахын тулд аппликейшнээ шинэчлэх шаардлагатай. Хэрвээ та Xcode-оос төхөөрөмж дээр ажиллуулж байгаа бол `node_modules/react-native/React/React.xcodeproj/project.pbxproj`  файл доторх `8081` гэснийг сонгосон портныхоороо болгож өөрчлөх шаардлагатай болно. 

### NPM түгжих алдаа

Хэрэв React Native CLI ашиглаж байх үед  `npm WARN locking Error: EACCES` гэх мэт алдаа гарвал доорхыг ажиллуулаад үзээрэй:

```
sudo chown -R $USER ~/.npm
sudo chown -R $USER /usr/local/lib/node_modules
```

### React-ын сан олдохгүй байх

Та төсөлдөө React Native-ыг дараа нь нэмсэн бол `RCTText.xcodeproj`, `RCTImage.xcodeproj` гэх мэт өөрийн ашиглаж буй холбогдох хамаарлуудыг нэмсэн эсэхээ шалгаарай. Эдгээрээс үүссэн binary-ууд нь таны аппын binary хэсэгтэй холбогдсон байх шаардлагатай. Xcode тохиргоо хэсэг дээрх `Linked Frameworks and Binaries` хэсгийг ашиглана уу. Нарийвчилсан зааврыг харах бол: [Сан холбох](linking-libraries-ios.md#content).

Хэрэв та  CocoaPods ашиглаж байгаа бол  React-ыг дэд -тай хамт `Podfile`-д нэмсэн эсэхээ нягтлаарай. Жишээ нь, та `<Text />`, `<Image />` болон `fetch()` API ашиглаж байгаа бол  `Podfile`.` дээрээ эдгээрийг нэмээрэй:

```
pod 'React', :path => '../node_modules/react-native', :subspecs => [
  'RCTText',
  'RCTImage',
  'RCTNetwork',
  'RCTWebSocket',
]
```

Дараа нь React суулгасан төсөлдөө `pod install`-ыг өгч, `Pods/` үүсгэсэн эсэхээ шалгаарай. CocoaPods нь `.xcworkspace`  файлыг хэрхэн ашиглах зааврыг өгөх ба суулгасан хамаарлыг ашиглах боломжтой болох юм. 

####  CocoaPod ашиглаж байгаа тохиолдолд React Native хөрвүүлдэггүй 

[cocoapods-fix-react-native](https://github.com/orta/cocoapods-fix-react-native) нэртэй CocoaPods plugin байдаг ба энэ нь хамаарлыг зохицуулахаас үүдэлтэй харилцан ялгаатай ажиллагааны улмаас эх кодыг дараа нь засахад тусалдаг.  

#### Аргумент жагсаалт хэт урт байна: толгойн өргөтгөл дахин хийх нь амжилтгүй боллоо

Төслийн Build Settings дотор `User Search Header Paths`  болон `Header Search Paths` нар нь Xcode хаанаас тухайн кодод дурдсан толгой файлуудыг `#import` хийх вэ гэдгийг зааж өгдөг. Pods-ын хувьд CocoaPods нь хайх фолдеруудыг заасан цаанаас байдаг массивыг ашигладаг. Энэхүү тохиргоо нь алдагдаагүй эсэхийг шалгаарай. Тохиргоо хийсэн фолдеруудын аль нь ч хэмжээний хувьд хэт том биш эсэхийг нягтлаарай. Хэрэв нэг фолдер нь хэт том байх юм бол  Xcode нь бүхэлд нь дахин хайлт хийх гэж оролддог ба дээрх алдааг өгөөд байдаг. 

`User Search Header Paths`, `Header Search Paths` хоёрын тохиргоог CocoaPods-ын тохируулсан анхны хэлбэрт шилжүүлэхийн тулд Build Settings дотор оруулсан зүйлийг сонгоод устгах гэснийг дарна. Ингэснээр оруулсан өөрчлөлтийг арилгах ба CocoaPod анхны хэлбэртээ шилжинэ.

### No transports available

React Native нь WebSockets-т polyfill ашигладаг. Эдгээр [polyfill](https://github.com/facebook/react-native/blob/master/Libraries/Core/InitializeCore.js) нь react-native модулийн нэг хэсэг болж эхэлдэг ба `import React from 'react'` ашиглан аппликейшндаа оруулдаг. Хэрэв [Firebase](https://github.com/facebook/react-native/issues/3645) гэх мэт WebSockets шаардах өөр модуль та ачаалах бол react-native ард үүнийг ачаалах/шаардах хэрэгтэй гэдгийг санаарай:

```
import React from 'react';
import Firebase from 'firebase';
```

## Shell команд хариу өгөхгүй байх тохиолдол

Хэрэв та энэ мэт ShellCommandUnresponsiveException-тэй таарвал:

```
Execution failed for task ':app:installDebug'.
  com.android.builder.testing.api.DeviceException: com.android.ddmlib.ShellCommandUnresponsiveException
```

`android/build.gradle` дотор [Gradle хувилбарыг 1.2.3 болгож бууруулаад](https://github.com/facebook/react-native/issues/2720) үзээрэй.

## react-native init hangs

Хэрэв та системдээ `react-native init` ажиллуулах үед алдаа гарвал [#2797](https://github.com/facebook/react-native/issues/2797) гэснийг харан verbose mode дээр дахин ажиллуулах гээд үзээрэй:

```
react-native init --verbose
```

## React-native package manager-ыг ажиллуулж эхлэх боломжгүй(Linux дээр)

### Кэйс 1: Алдаа "код":"ENOSPC","errno":"ENOSPC"

Хэд хэдэн директороос шалтгаалан үүсгэн алдааг[inotify](https://github.com/guard/listen/wiki/Increasing-the-amount-of-inotify-watchers) (Linux дээр watchman  ашигладаг) хянах боломжтой. Үүнийг шийдэхийн тулд терминал дээрээ уг командыг өгнө.


```
echo fs.inotify.max_user_watches=582222 | sudo tee -a /etc/sysctl.conf && sudo sysctl -p
```
