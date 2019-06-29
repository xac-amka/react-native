---
id: running-on-device
title: Төхөөрөмж дээр ажиллуулах
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
  .display-os-mac .toggler .button-mac,
  .display-os-linux .toggler .button-linux,
  .display-os-windows .toggler .button-windows,
  .display-platform-ios .toggler .button-ios,
  .display-platform-android .toggler .button-android {
    background-color: #05A5D1;
    color: white;
  }
  block { display: none; }
  .display-platform-ios.display-os-mac .ios.mac,
  .display-platform-ios.display-os-linux .ios.linux,
  .display-platform-ios.display-os-windows .ios.windows,
  .display-platform-android.display-os-mac .android.mac,
  .display-platform-android.display-os-linux .android.linux,
  .display-platform-android.display-os-windows .android.windows {
    display: block;
  }
</style>

Аппаа хэрэглэгчдэд хүргэхийн өмнө тест хийж үзэх нь зүйтэй. React Native аппаа нэг төхөөрөмж дээр хэрхэн ажиллуулж үзэн, бэлэн болгох вэ гэдгийг энд зааж өгсөн болно.

Хэрэв та Expo CLI эсвэл Create React Native App ашиглан төслөө хийсэн бол та төхөөрөмж дээрээ Expo app доторх QR кодыг скан хийн аппаа урьдчилан харах боломжтой. Аливаа нэг төхөөрөмж дээр аппаа ажиллуулж, бэлэн болгохын тулд та [Эхлэх заавар](getting-started.md) гэснээс натив кодын dependencies-ыг суулгах шаардлагатай. 

<div class="toggler">

  <ul role="tablist" >
    <li id="ios" class="button-ios" aria-selected="false" role="tab" tabindex="0" aria-controls="iostab" onclick="displayTab('platform', 'ios')">
      iOS
    </li>
    <li id="android" class="button-android" aria-selected="false" role="tab" tabindex="-1" aria-controls="androidtab" onclick="displayTab('platform', 'android')">
      Android
    </li>
  </ul>
</div>

<block class="linux windows mac ios" />

## iOS төхөөрөмж дээр аппаа ажиллуулах

<block class="linux windows mac android" />

## Android төхөөрөмж дээр аппаа ажиллуулах

<block class="linux windows mac ios android" />

<div class="toggler">
<span>Development OS:</span>
<a href="javascript:void(0);" class="button-mac" onclick="displayTab('os', 'mac')">macOS</a>
<a href="javascript:void(0);" class="button-linux" onclick="displayTab('os', 'linux')">Linux</a>
<a href="javascript:void(0);" class="button-windows" onclick="displayTab('os', 'windows')">Windows</a>
</div>

<block class="linux windows ios" />

iOS төхөөрөмжид зориулж апп хийх бол танд Mac шаардлагатай. Эсвэл та Expo CLI ашиглан Expo client апп дээр аппаа хэрхэн ажиллуулахыг мэдэхийг хүсвэл [Эхлэх заавах ](getting-started.md) гэснийг уншина уу.
<block class="mac ios" />

### 1. USB ашиглан төхөөрөмжөө холбох

iOS төхөөрөмжөө USB ашиглан Mac-тай холбоно. Төслийнхөө `ios`  гэсэн фолдерт хандан `.xcodeproj` файлыг нээнэ. Хэрэв та CocoaPods ашигласан бол Xcode ашиглан `.xcworkspace`-ыг нээнэ үү. 

Хэрэв та анх удаа аппаа iOS төхөөрөмж дээр ажиллуулах гэж байгаа бол та төхөөрөмжөө бүртгүүлэх хэрэгтэй болно. Xcode цэсээс **Product** гэснийг сонгоод **Destination** гэсэн рүү хандана. Тэндээсээ төхөөрөмжөө хайж олон сонгоно. Xcode төхөөрөмжийг чинь бүртгэх болно. 

### 2. Код тохиргоо хийх

[Apple хөгжүүлэгчийн аккаунт](https://developer.apple.com/) байхгүй бол шинээр бүртгүүлээрэй.

Xcode Project Navigator дотроо өөрийн төслөө сонгоод гол таргет файлаа сонгоно (төсөлтэй чинь ижилхэн нэртэй байх хэрэгтэй). тэгээд  "General" гэснийг олоод "Signing" гэж ороод Apple хөгжүүлэгчийн аккаунт эсвэл баг чинь Team гэсэн цэсэнд байгаа эсэхийг харна уу. Таргет файлыг шалгахад мөн адилхан үйлдэл хийнэ (Tests гэж төгссөн байх ба гол таргетийн доор байна).

![](/react-native/docs/assets/RunningOnDeviceCodeSigning.png)

### 3. Аппаа хийж, ажиллуулах

Хэрэв бүх тохиргоо нь зөв хийгдсэн бол таны төхөөрөмж Xcode toolbar дээр build target гэж орсон байна. Мөн Төхөөрөмжүүд гэсэн (`⇧⌘2`) хэсэг дээр харагдана. Одоо та **Build and run** товчийг (`⌘R`) даран эсвэл **Product** цэсээс **Run** гэснийг сонгож болно. Таны апп төхөөрөмж дээр чинь тун удахгүй ажиллах болно. 

![](/react-native/docs/assets/RunningOnDeviceReady.png)

> Хэрэв танд ямар нэг асуудал тулгарвал Apple-ын [Төхөөрөмж дээр аппаа ажиллуулж эхлүүлэх](https://developer.apple.com/library/content/documentation/IDEs/Conceptual/AppDistributionGuide/LaunchingYourApponDevices/LaunchingYourApponDevices.html#//apple_ref/doc/uid/TP40012582-CH27-SW4) гэснийг уншина уу. 

<block class="mac windows linux android" />

### 1. USB-гээр дибаг хийхийг идэвхжүүлэх

Ихэнх Android төхөөрөмж цаанаасаа зөвхөн Google Play-ээс татсан аппыг суулгаж, ажиллуулах тохиргоотой байдаг. Та хөгжүүлэлт хийж байх үедээ аппаа суулгахыг хүсвэл USB дибаг хийхийг идэвхжүүлэх хэрэгтэй.  

Төхөөрөмж дээрээ USB дибаг хийхийг идэвхжүүлэхийг хүсвэл та эхлээд **Settings** → **About phone**  гэж ороод "Developer options"  цэсийг идэвхжүүлэх хэрэгтэй.  Тэгээд доор байх `Build number` гэсэн дээр долоон удаа дарна. Та тэгээд **Settings** → **Developer options** гэж ороод "USB debugging" гэснийг идэвхжүүлнэ. 

### 2. USB ашиглан төхөөрөмжөө залгах 

React Native төслөө Android төхөөрөмж дээр ажиллуулахын тулд ямар тохиргоо хийхийг харъя. USB ашиглан төхөөрөмжөө хөгжүүлэлт хийсэн төхөөрөмжтэйгөө холбоорой. 

<block class="linux android" />

Дараа нь `lsusb` ашиглан (Mac дээр [lsusb суулгах](https://github.com/jlhonora/lsusb)) үйлдвэрлэгчийн кодыг шалгана. 
 `lsusb` нь үүн шиг зүйл байна:

```bash
$ lsusb
Bus 002 Device 002: ID 8087:0024 Intel Corp. Integrated Rate Matching Hub
Bus 002 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 001 Device 003: ID 22b8:2e76 Motorola PCS
Bus 001 Device 002: ID 8087:0024 Intel Corp. Integrated Rate Matching Hub
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 004 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 003 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
```

Эдгээр мөрнүүд нь таны төхөөрөмжтэй холбогдсон USB төхөөрөмжүүдийг харуулж буй юм. 

Таны утасны мэдээллийг харуулсан мөрийг та эндээс олох хэрэгтэй. Хэрэв эргэлзэж байвал, утсаа салгаад дахиад команд өгөөд үзээрэй:

```bash
$ lsusb
Bus 002 Device 002: ID 8087:0024 Intel Corp. Integrated Rate Matching Hub
Bus 002 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 001 Device 002: ID 8087:0024 Intel Corp. Integrated Rate Matching Hub
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 004 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 003 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
```

Утсаа салгасны дараа тухайн утасны моделийн мэдээллийг харуулж байсан мөр нь (энэ тохиолдолд "Motorola PCS" ) жагсаалтаас арилсан байгааг харж байна. Энэ мөр бидэнд хэрэгтэй гэсэн үг. 

`Bus 001 Device 003: ID 22b8:2e76 Motorola PCS`

Дээрх мөрнөөс та төхөөрөмжийн ID-ын эхний дөрвөн орныг авна: 

`22b8:2e76`

Энэ жишээ дээр бол `22b8` гэсэн үг. Motorola-ыг таних код бол энэ юм. 

Та аппаа ажиллуулахын тулд энэ мэдээллийг udev rules  дотроо хийх хэрэгтэй:

```sh
echo 'SUBSYSTEM=="usb", ATTR{idVendor}=="22b8", MODE="0666", GROUP="plugdev"' | sudo tee /etc/udev/rules.d/51-android-usb.rules
```
Дээрх командыг өгөхдөө `22b8` гэснийг олсон таних мэдээллээрээ солих хэрэгтэй. 

<block class="mac windows linux android" />

Одоо төхөөрөмж чинь Android Debug Bridge буюу ADB-аар зав холбогдсон эсэхийг шалгахаар `adb devices`-ыг ажиллуулна. 

```
$ adb devices
List of devices attached
emulator-5554 offline   # Google emulator
14ed2fcc device         # Physical device
```

Баруун баганад `device` гэж харагдаж байвал уг төхөөрөмж холбогдсон гэсэн үг. Та нэг удаад  **зөвхөн нэг төхөөрөмж холбох** боломжтой. 

### 3. Аппаа ажиллуулах

Command prompt дээрээ доорхыг шивээд төхөөрөмж дээрээ аппаа суулган, ажиллуулаарай:

```
$ react-native run-android
```

> Хэрэв "bridge configuration isn't available" гэсэн алдаа өгч байвал [Adb reverse ашиглах](running-on-device.md#method-1-using-adb-reverse-recommended) гэснийг уншина уу.  

> Зөвлөмж
>
> Та мөн `React Native CLI` ашиглан `Release` build-ыг гаргаж, ажиллуулах боломжтой (жишээ нь `react-native run-android --variant=release`).

<block class="mac windows linux android ios" />

<block class="mac ios" />

## Хөгжүүлэлтийн сервертэй холбох

Та мөн хөгжүүлэлтийн сервер ашиглан төхөөрөмж дээр хурдан давтах боломжтой. Танд ердөө компьютертойгоо ижил  Wi-Fi-д холбогдсон байх шаардлагатай.[Developer menu](debugging.md#accessing-the-in-app-developer-menu)-ыг нээхийн тулд төхөөрөмжөө сэгсрэх хэрэгтэй. Тэгээд Live Reload гэснийг идэвхжүүлнэ. JavaScript код өөрчлөгдөх бүрт таны апп дахин ачаалах болно. 

![](/react-native/docs/assets/DeveloperMenu.png)

### Асуудлыг шийдэх

> Хэрэв ямар нэг асуудал гарвал таны Mac болон бусад төхөөрөмж чинь ижил сүлжээнд холбогдон, нэг нэгэнтэйгээ мэдээлэл солилцож болохоор байгаа эсэхийг шалгаарай. Нээлттэй ашиглаж болох утасгүй сүлжээнүүдийн ихэнх нь сүлжээ дэх бусад төхөөрөмж рүү хандахаас сэргийлсэн тохиргоотой байдаг. Та энэ тохиолдолд  Personal Hotspot гэсэн функцийг ашиглах боломжтой. 

Хөгжүүлэлтийн сервертэй холбогдох гэхэд [алдаа бүхий улаан дэлгэц](debugging.md#in-app-errors-and-warnings) гарч ирэх магадлалтай ба ийм бичиг гарна:

> [http://localhost:8081/debugger-proxy?role=client]() холбогдох хугацаа дууссан байна. Та node proxy ажиллуулж байна уу? 
Хэрэв та төхөөрөмж дээр ажиллуулж байгаа бол `RCTWebSocketExecutor.m` дотор зөв IP хаяг байгаа эсэхийг шалгана уу.

Энэ асуудлыг хэрхэн шийдэх тухай дараах хэсгээс харна уу. 

#### 1. Wi-Fi сүлжээ

Таны лаптоп болон гар утас чинь **ижил** Wi-Fi сүлжээнд холбогдсон эсэхийг шалгана уу. 

#### 2. IP хаяг

Таны төхөөрөмж дээр скрипт нь IP хаягийг тань зөв таньсан эсэхийг шалгана уу (жишээ нь 10.0.1.123)

![](/react-native/docs/assets/XcodeBuildIP.png)

**Report navigator** табийг нээн сүүлийн **Build** -ыг сонгон `xip.io` гэснийг хайж олно. Апп дээрх IP хаяг нь таны төхөөрөмжийн IP хаяг болон `.xip.io` домэйнтай таарч байх ёстой (жишээ нь 10.0.1.123.xip.io).

#### 3. Сүлжээ/рүтэр тохируулах

React Native нь таны төхөөрөмжийг танихдаа  DNS service **xip.io** ашигладаг. Учир нь Apple ATS нь домэйн нэр биш IP хаяг бүхий URL-уудыг хориглодог ба хөгжүүлэгчийн сүлжээ нь local host нэрийг тохируулдаггүй. Зарим рүтэр нь local IP хүрээний аливаа асуудлыг DNS Servers шийдэхээс сэргийлсэн аюулгүй функцтэй байдаг. 

`nslookup` ажиллуулан  xip.io-ын асуудлыг шийдэх боломжтой эсэхийг харъя. 

```bash
$ nslookup 10.0.1.123.xip.io
```

Хэрэв таны local IP хаягийн асуудлыг шийдэж чадахгүй бол  **xip.io** үйлчилгээ нь унтарсан эсвэл рүтер хязгаарлаад байна гэсэн үг. 

Рүтэрийн гадуур xip.io-ыг ашиглахын тулд:

- Google DNS (8.8.8.8) ашиглахаар утасны тохиргоо хийнэ
- Рүтэр дээрээ холбогдох аюулгүй байдлыг функцийг идэвхгүй болгоно

<block class="mac windows linux android" />

## Хөгжүүлэгчийн сервертэй холбох 

Та мөн хөгжүүлэлт хийсэн машин дээрээ хөгжүүлэгчийн серверийг холбон ажиллуулж аливаа нэг төхөөрөмж дээр хурдан дахин ажиллуулах боломжтой. Танд USB кабел, Wi-Fi сүлжээ байгаа эсэхээс хамаарч үүнийг хийх хэд хэдэн арга байна. 


### Арга 1: adb reverse ашиглах (энэ аргыг ашиглахыг санал болгож байна)

<block class="mac windows linux android" />

Хэрэв таны төхөөрөмж Android 5.0 (Lollipop) эсвэл үүнээс сүүлийн хувилбарыг ашиглаж байгаа, USB дибаг идэвхжүүлсэн бөгөөд хөгжүүлэлт хийсэн машинтай USB-ээр холбогдсон бол та энэ аргыг ашиглах боломжтой. 

<block class="mac windows linux android" />

Command prompt дээр доорхыг ажиллуул:

```
$ adb -s <device name> reverse tcp:8081 tcp:8081
```

Төхөөрөмжийнхөө нэрийг хайж олохын тулд доорх adb командыг өгнө үү:

```
$ adb devices
```

Та [Хөгжүүлэгчийн цэс](debugging.md#accessing-the-in-app-developer-menu) шууд дахин ачаалах (Live Reload) функцыг одоо идэвхжүүлж болно. JavaScript код өөрчлөгдөх бүрт таны апп дахин ачаална. 

### Арга 2: Wi-Fi ашиглан холбох 

Та Wi-Fi ашиглан хөгжүүлэлтийн сервертэй холбогдох боломжтой. Эхлээд та USB кабел ашиглан төхөөрөмж дээрээ аппаа суулгах хэрэгтэй. Нэгэнт холбосон бол дараа нь доорх зааврын дагуу утасгүйгээр дибаг хийх боломжтой. Танд эхлээд хөгжүүлэлт хийсэн машины одоогийн IP хаяг хэрэг болно. 

<block class="mac android" />

**System Preferences** → **Network** дээрээс IP хаягийг харах боломжтой. 

<block class="windows android" />

Command prompt-оо нээгээд `ipconfig` гэж бичээд машиныхаа IP хаягийг олно ([нэмэлт мэдээлэл](http://windows.microsoft.com/en-us/windows/using-command-line-tools-networking-information)).

<block class="linux android" />

Терминалаа нээгээд `/sbin/ifconfig` гэж бичин машиныхаа IP хаягийг олно .

<block class="mac windows linux android" />

1. Таны компьютер, утас нэг **ижил** Wi-Fi сүлжээнд холбогдсон эсэхийг шалгана уу. 
2. Төхөөрөмж дээрээ React Native аппаа нээнэ үү. 
3. Танд [алдаа заасан улаан дэлгэц](debugging.md#in-app-errors-and-warnings) харагдана. Санаа зоволтгүй. Доорх алхам нь үүнийг засах болно.  
4. Апп доторх [Хөгжүүлэгчийн цэс](debugging.md#accessing-the-in-app-developer-menu)-ийг нээнэ.
5. **Dev Settings** → **Debug server host & port for device** гэсэн рүү оч.
6. Машиныхаа IP хаяг болон local dev server (10.0.1.1:8081 г.м) бичнэ.
7.  **Developer menu** рүү буцаж очин **Reload JS** сонгоно.

Та [Хөгжүүлэгчийн цэс](debugging.md#accessing-the-in-app-developer-menu) Шууд дахин ачаалах функцыг одоо идэвхжүүлж болно. JavaScript код өөрчлөгдөх бүрт таны апп дахин ачаална. 

<block class="mac ios" />

## Аппаа гаргахад бэлэн болгох

Та React Native ашиглан гайхалтай апп хийлээ гэж бодъё. Одоо тэгээд App Store дээр гаргах гээд тэсэн ядаж байгаа байх. Гаргах явц нь бусад натив iOS апптай л адил байна. Гэхдээ нэмэлт хэдэн зүйлсийг бодолцох хэрэгтэй. 

> Хэрэв та Expo ашиглаж байгаа бол Expo Guide-ыг уншина уу [Бие даасан апп гаргах](https://docs.expo.io/versions/latest/distribution/building-standalone-apps/).

### 1. Апп хамгаалалтыг идэвхжүүлэх 

App Transport Security (ATS) нь iOS 9 дээр гарсан функц бөгөөд HTTPS дагуу илгээгдээгүй HTTP хүсэлтүүдийг няцаадаг. Үүний улмаас  HTTP урсгал блок хийгдэхэд хүрдэг. Хөгжүүлэлт хийсэн React Native сервер ч үүнд өртөнө. Хөгжүүлэлт хийх ажлыг илүү хялбар болгох үүднээс цаанаасаа React Native төслүүд дээр `localhost`-д ATS-ыг идэвхгүй болгосон байдаг.

Та `ios/` фолдерын `Info.plist` файл доторх `NSExceptionDomains` дотроос `localhost`-ыг арилган апп гаргахаар бэлтгэхийн өмнө ATS-ыг дахин идэвхжүүлэх хэрэгтэй. Мөн та Info цонх дахь target properties-ыг нээн App Transport Security тохиргоог өөрчлөн Xcode дахь ATS-ыг дахин идэвхжүүлж болно. 

>Хэрэв таны аппликейшн бэлэн гарах үед HTTP хүсэлтэд хандах хэрэгтэй бол [энэ нийтлэлээс](http://ste.vn/2015/06/10/configuring-app-transport-security-ios-9-osx-10-11/) ATS тохиргоог хэрхэн хийх тухай уншаарай.

### 2. Бэлэн гаргах төлөвийг тохируулах

App Store дээр бэлэн гаргах аппаа тохируулахын тулд Xcode дээр `Release` scheme-ыг ашиглах шаардлагатай. `Release` хийхээр хийсэн  апп нь автоматаар апп доторх Хөгжүүлэгчийн цэсийг идэвхгүй болгосон байна. Ингэснээр апп бэлэн болох үед хэрэглэгчид санамсаргүйгээр цэс рүү орохоос сэргийлнэ. JavaScript кодыг дотоод сүлжээнд суулгаж өгөх ба та аливаа нэг төхөөрөмж дээр аппаа суулгаж, компьютертой холбоогүй ч тест хийж үзэх боломжтой юм. 

`Release` scheme ашиглан гаргах аппынхаа тохиргоог хийхийн тулд **Product** → **Scheme** → **Edit Scheme** гэж орно. Хажуу талын хэсгээс **Run** гэдгийг сонгоно. Тэгээд Build Configuration гэснээс `Release` гэдгийг сонгон тохируулна. 


![](/react-native/docs/assets/ConfigureReleaseScheme.png)

#### Мэргэжлийн зөвлөгөө


Таны аппын хэмжээ нэмэгдэх тусам эхлэх дэлгэц шилжих үед цагаан гэрэл анивчин харагдаж, үндсэн аппликейшны харагдац нь гарч ирэх зүйл ажиглагдана. Хэрэв ийм зүйл тохиолдвол дэлгэц хооронд шилжих үед эхлэх дэлгэцийг харуулдаг байлгая гэвэл доорх кодыг  `AppDelegate.m` руу нэмээрэй. 

```objc
  // Place this code after "[self.window makeKeyAndVisible]" and before "return YES;"
  UIView* launchScreenView = [[[NSBundle mainBundle] loadNibNamed:@"LaunchScreen" owner:self options:nil] objectAtIndex:0];
  launchScreenView.frame = self.window.bounds;
  rootView.loadingView = launchScreenView;
```
Төхөөрөмж дээр ажиллуулах үед тогтмол багц гарч байдаг. Дибаг хийхэд ч гэсэн. Хэрэв та цаг хэмнэхийг хүсвэл Debug-ын багц гаргах үйлдлийг унтраах боломжтой. Ингэхдээ Xcode Build Phase `Bundle React Native code and images` дотор доорхыг нэмж өгнө:

```shell
 if [ "${CONFIGURATION}" == "Debug" ]; then
  export SKIP_BUNDLING=true
 fi
```

### 3. Аппаа бэлэн гаргах 

`⌘B` гэж дарах эсвэл цэсний хэсгээс  **Product** → **Build**  гэж сонгон та аппаа бэлэн гаргах боломжтой. Гаргахад бэлэн болсон тохиолдолд та бета шалгагч руу илгээн, App Store руу оруулах боломжтой болно. 

> Мөн та `--configuration`  гэсэн сонголтыг `Release` (`react-native run-ios --configuration Release` г.м)-тэйгээр хамт хэрэглэн `React Native CLI`-ыг ашиглан энэ үйлдлийг гүйцэтгэх боломжтой. 

<block class="mac windows linux android" />

## Аппаа ажиллуулахад бэлэн болгох

Та React Native ашиглан гайхалтай апп хийлээ гэж бодъё. Одоо тэгээд Play Store дээр гаргах гээд тэсэн ядаж байгаа байх. Гаргах явц нь бусад натив Android апптай л адил байна. Гэхдээ нэмэлт хэдэн зүйлсийг бодолцох хэрэгтэй. Илүү дэлгэрэнгүй унших бол [generating a signed APK](signed-apk-android.md) гэснийг харна уу.


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
