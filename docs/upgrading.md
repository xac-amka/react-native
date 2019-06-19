---
id: upgrading
title: React Native-ын шинэ хувилбарт шилжих
---

React Native-ын шинэ хувилбарт шилжсэнээр та илүү олон API, харагдац, хөгжүүлэгчийн хэрэгслүүд болон бусад зүйлсийг ашиглах боломжтой болно. Шинэ хувилбарт шилжихэд амар бөгөөд бид ч үүнийг аль болох хялбархан байхаар хийж өгсөн.

## Expo төслүүд

Expo төслөө React Native-ын шинэ хувилбарт шилжүүлэхийн тулд `package.json` файл дахь `react-native`, `react`, `expo` пакэжийн хувилбаруудаа шинэчлэх шаардлагатай. [Энэхүү жагсаалтаас](https://docs.expo.io/versions/latest/sdk/#sdk-version) ямар хувилбаруудыг дэмждэг болохыг хараарай. Мөн та `app.json`  файлдаа `sdkVersion`-ыг зөв тохируулж өгөх хэрэгтэй. 

Хэрхэн төслөө шинэчлэх тухай сүүлийн үеийн мэдээллийг [SDK ашиглан Expo шинэчлэх](https://docs.expo.io/versions/latest/workflow/upgrading-expo-sdk-walkthrough) гэснээс уншаарай.

## React Native projects

Ердийн React Native төслүүд нь Android, iOS болон JavaScript төслүүдийг агуулсан байдаг тул шинэчлэл хийхэд түвэгтэй байх нь бий. React Native-ыг хуучин хувилбарыг шинэчлэхийн тулд та эдгээрийг хийх хэрэгтэй. 

### Git ашиглан шинэчлэх

[React Native CLI](https://github.com/react-native-community/react-native-cli) нь `upgrade` командтай байх ба энэ нь эх файлыг  нэг үйлдлээр л шинэчлэх боломж олгодог. [rn-diff-purge](https://github.com/react-native-community/rn-diff-purge) үүнд тусалдаг.


#### 1. Төсөлдөө Git ашиглах

> Git ашиглаагүй төслүүдэд л энэхүү алхам хамаатай болно. Хэрэв Git ашигладаг бол үүнийг алгасаарай. 
Хэрэв таны төсөлд Git-ын хувилбарт систем ажилладаггүй бол Mercurial, SVN ашиглах эсвэл юу ч ашиглахгүй байж бас болно. Та гэхдээ `react-native upgrade` ашиглахын тулд систем дээрээ [Git суулгах](https://git-scm.com/downloads) шаардлагатай.
Git нь `PATH` дээр мөн байх хэрэгтэй. Хэрэв төсөл тань Git ашигладаггүй бол эхлүүлээд commit хийгээрэй:

```sh
git init
git add .
git commit -m "upgrade RN"
```

Шинэчлэх процесс дуусаж, аливаа асуудалгүй болсны дараа та `.git`-ыг арилгаж болно. 

#### 2. `upgrade` командыг ажиллуулах

Сүүлийн хувилбарт шилжихийн тулд доорх командыг өгөөрэй:

```sh
react-native upgrade
```

Та `0.59.0-rc.0` гэхчлэн React Native-ын тодорхой хувилбарт шинжлэхээ зааж өгөх боломжтой:

```sh
react-native upgrade 0.59.0-rc.0
```

Энэ төсөл нь `git apply`-ыг ашиглан 3 замт холболтоор шинэчлэгдэнэ. Тиймээс ямар асуудал зөрчил гарвал тэрийг нь засах хэрэгтэй.

#### 4. Асуудал зөрчлийг шийдэх

Асуудалтай файлууд нь өгөгдлийн хязгаарлагч агуулсан байх ба өөрчлөлт хаана байгааг тодорхой харуулдаг. Жишээлбэл:

```
13B07F951A680F5B00A75B9A /* Release */ = {
  isa = XCBuildConfiguration;
  buildSettings = {
    ASSETCATALOG_COMPILER_APPICON_NAME = AppIcon;
<<<<<<< ours
    CODE_SIGN_IDENTITY = "iPhone Developer";
    FRAMEWORK_SEARCH_PATHS = (
      "$(inherited)",
      "$(PROJECT_DIR)/HockeySDK.embeddedframework",
      "$(PROJECT_DIR)/HockeySDK-iOS/HockeySDK.embeddedframework",
    );
=======
    CURRENT_PROJECT_VERSION = 1;
>>>>>>> theirs
    HEADER_SEARCH_PATHS = (
      "$(inherited)",
      /Applications/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/include,
      "$(SRCROOT)/../node_modules/react-native/React/**",
      "$(SRCROOT)/../node_modules/react-native-code-push/ios/CodePush/**",
    );
```

"Бидний" гэдэг нь "танай баг"-ийг харин "тэдний" гэдэг нь "React Native хөгжүүлэгчийн баг"-ийг хэлж байна гэж ойлгоорой. 

### Өөр арга

Зөвхөн дээрх арга болохгүй бол ашиглаарай.

#### 1. `react-native` dependency шинэчлэх

`react-native` npm пакэжийн сүүлийн хувилбарыг [эндээс](https://www.npmjs.com/package/react-native) шалгах (эсвэл`npm info react-native` ашиглаж шалгаарай).

Одоо `npm install --save` ашиглан `react-native` хувилбарыг суулгаарай:

```sh
$ npm install --save react-native@X.Y
# where X.Y is the semantic version you are upgrading to
npm WARN peerDependencies The peer dependency react@~R included from react-native...
```

Хэрэв peerDependency-ын анхааруулга гарч ирвэл `react`-аа шинэчлээрэй:

```sh
$ npm install --save react@R
# where R is the new version of react from the peerDependency warning you saw
```

#### 2. Төслийнхөө template-ыг шинэчлэх

Шинэ npm пакэж нь `react-native init`-ыг ажиллуулахад гарч ирдэг файлуудын шинэ хувилбаруудыг агуулсан байдаг. Тухайлбал, iOS болон Android дэд төслүүд дээр.

Та [rn-diff-purge](https://github.com/pvinis/rn-diff-purge)-руу орж template файлуудад өөрчлөлт орсон эсэхийг хараарай. 
Ямар нэг өөрчлөлт байхгүй бол шууд төслөө хийж, хөгжүүлэлтээ үргэлжлүүлээрэй. Зарим нэг жижиг өөрчлөлт орсон бол та өөрөө шинэчлэн, дахин хийх хэрэгтэй болно. 

Хэрэв их өөрчлөлт байх юм терминал дээр үүнийг ажиллуулаарай:

```sh
$ react-native upgrade
```
Энэ нь сүүлийн template-тай таны файлууд зохицож байгаа эсэхийг шалгаж, доорх үйлдлийг хийдэг:

- Хэрэв template дотор шинэ файл байх юм бол шууд үүсгэнэ.
- Хэрэв template дотор файлтай чинь төстэй файл байх юм бол алгасна. 
- Хэрэв төсөл дэх файл чинь template-д байгаагаас өөр байх юм бол таныг файлаа хадгалах эсвэл тухайн template-ын хувилбараар сольж бичих сонголт өгнө. 

## Өөрөө шинэчлэх

Зарим шинэчлэлийг заавал өөрөө  0.28-аас 0.29, эсвэл 0.56-аас 0.57 гэх мэтээр шинэчлэх хэрэгтэй болдог. Шинэ хувилбарт шилжих гэж байгаа бол [шинэ хувилбарын мэдээлэл](https://github.com/facebook/react-native/releases)-тэй танилцаж, таны төсөлд ямар өөрчлөлтийг өөрөө бичиж оруулах хэрэгтэй тухай уншаарай.

