---
id: debugging
title: Алдаа засах

---

## Keyboard shortcut-ыг идэвхжүүлэх

iOS Симулятор дээр React Native нь цөөн хэдэн keyboard shortcut дэмждэг. Энэ тухай доор тайлбарласан болно. Идэвхжүүлэхийн тулд, Hardware цэсийг нээн Keyboard-г сонгоно. “Contact Hardware Keyboard” гэсэн нь зөвлөгдсөн байх ёстойг анхаарна уу. 

## App доторх Хөгжүүлэгчийн цэст хандах

Та iOS  төхөөрөмжөө сэгсэрснээр эсвэл Hardware цэс дотроос “Shake Gesture”-ыг сонгон Хөгжүүлэгчийн цэст хандах боломжтой. Мөн апп тань iOS cимулятор дээр ажиллаж байгаа бол `⌘D`  гэсэн товчлолыг ашиглах эсвэл МАК үйлдлийн систем дээр Android эмулятор дээр ажиллаж байгаа бол `⌘M` гэсэн товчлолыг, Windows болон Linux дээр `Ctrl+M` дарж хандаж болно. Эсвэл Android дээр хөгжүүлэгчийн цэсийг нээхийн тулд `adb shell input keyevent 82` гэсэн команд өгөх боломжтой (82 гэдэг нь цэсний түлхүүр код нь юм).

![](/react-native/docs/assets/DeveloperMenu.png)

> Шинээр гаргах (хийх явцад) хөгжүүлэгчийн цэс нь идэвхгүй байдаг. 

## JavaScript дахин ачаалах

Аппдаа өөрчлөлт хийх болгондоо дахин хөрвүүлж байхын оронд та JavaScript кодыг шууд дахин ачаалж болно. Ингэхийн тулд
Хөгжүүлэгчийн цэсээс "Reload" гэснийг сонгоно. Мөн iOS Симулятор дээр `⌘R` гэснийг дарах эсвэл Android эмулятор дээр хоёр удаа `R` дарж дахин ачаалж болно.

### Автоматаар дахин ачаалах

Таны код өөрчлөгдөх тутамд автоматаар дахин ачаалах тохиргоо байдаг бөгөөд үүнийг идэвхжүүлснээр хөгжүүлэлтийг хурдан хийх боломжтой болно. Идэвхжүүлэхийн тулд Хөгжүүлэгчийн цэсээс “Enable Live Reload" гэснийг сонгоно.

Бүр цаашлаад аппаа ажиллаж байх үед JavaScript bundle дахь файлуудаа автоматаар шинэчилж байхаар тохируулах бол Хөгжүүлэгчийн цэсээс [Hot Reloading](https://facebook.github.io/react-native/blog/2016/03/24/introducing-hot-reloading.html) гэдгийг идэвхжүүлнэ. Ингэснээр дахин ачаалсан ч аппын төлөвийг хадгалахад туслах юм.

> Зарим үед hot reloading төгс ажиллахгүй байх тохиолдол гардаг . Ямар нэг асуудал гарвал full reload хийн аппаа шинээр ажиллуулах хэрэгтэй.

Тодорхой нөхцөлд та хийсэн өөрчлөлтөө хадгалахын тулд аппаа rebuild хийх хэрэгтэй болдог:

-  iOS дээр `Images.xcassets`-д зураг нэмэх эсвэл Android дээр `res/drawable` хавтас нэмэх гэх мэт натив аппдаа шинэ нөөц нэмсэн бол,

- Натив кодыг өөрчилсөн бол (iOS дээр Objective-C/Swift эсвэл Android дээр Java/C++).

## Апп доторх алдаа болон анхааруулга

Апп хөгжүүлэлт хийгдэж байх үед алдаа, анхааруулга дэлгэц дээр гарч ирнэ.

### Алдаанууд

Апп доторх алдаануудын тухай мэдээлэл улаан өнгийн суурьтайгаар, дэлгэц дүүрэн гарч ирдэг. Энэ дэлгэцийг RedBox гэж нэрлэдэг. `console.error()` гэснийг ашиглан туршиж үзэж болно.

### Анхааруулга

Анхааруулга нь дэлгэц дээр шар өнгийн суурьтай харагддаг. Эдгээр анхааруулгыг YellowBoxes гэж нэрлэдэг. Анхааруулга дээр дарж дэлгэрэнгүй мэдээлэл харж болно. Эсвэл тоохгүй орхиж болно.

RedBox-ийн нэгэн адил та `console.warn()` ашиглан YellowBox-ыг гаргаж туршиж боломжтой.

Хөгжүүлэлтийн явцад `console.disableYellowBox = true;` гэдгийг ашиглан YellowBox-ыг идэвхгүй болгож болно. 

Тодорхой анхааруулгыг програмчлан тоохгүй орхидог болгож болно. Ингэхдээ тоолгүй орхих prefix-ийн массивийг тохируулна:

```javascript
import {YellowBox} from 'react-native';
YellowBox.ignoreWarnings(['Warning: ...']);
```

`IS_TESTING`  орчны хувьсагчийн тохируулан CI/Xcode, YellowBoxes-ыг идэвхгүй болгож болно.

> RedBoxes болон YellowBoxes нь апп бэлэн болох үед автоматаар идэвхгүй болдог. 

## Chrome Developer Tools

Chrome-д JavaScript-ын кодын алдааг засахдаа Хөгжүүлэгчийн Цэсээс "Debug JS Remotely" гэдгийг сонгоно. Ингэснээр  [http://localhost:8081/debugger-ui](http://localhost:8081/debugger-ui) гэсэн шинэ цонх нээгдэнэ.

[Developer Tools](https://developer.chrome.com/devtools) нээхдээ Chrome Menu-гээс `Tools → Developer Tools`  гэдгийг сонгоно. 
Мөн гар товчлуур ашиглан (macOS дээр `⌘⌥I` , Windows дээр `Ctrl` `Shift` `I` ) DevTools-руу нэвтрэх боломжтой. Алдаа засах явцыг илүү үр дүнтэй болгохыг хүсвэл [Pause On Caught Exceptions](http://stackoverflow.com/questions/2233339/javascript-is-there-a-way-to-get-chrome-to-break-on-all-errors/17324511#17324511) гэдгийг ашиглах нь зүйтэй.

> Тэмдэглэл: React Developer Tools Chrome өргөтгөл нь React Native-т ажилладаггүй, гэхдээ та оронд нь дангаар ажилладаг хувилбарыг нь ашиглах боломжтой. Хэрхэн ашиглах тухай[эндээс](debugging.md#react-developer-tools) уншина уу.

### JavaScript тусгай алдаа засагчийг ашиглан алдаа засах

Chrome Developer Tools-ын оронд JavaScript-ын тусгай алдаа засагчийг ашиглахын тулд `REACT_DEBUGGER` орчны хувьсагчийг тохируулах команд өгвөл тусгаа алдаа засагч ажиллаж эхэлнэ. Тэгээд алдаа засах ажлыг эхлүүлэхдээ Хөгжүүлэгчийн Цэсээс "Debug JS Remotely"  гэдгийг сонгоно. 

Алдаа засаг нь бүх жагсаалтыг үндсээр нь зайгаар тусгаарласан байдлаар хүлээн авдаг. Жишээ нь алдаа засагчийг ажиллуулж эхлэхийн тулд та `REACT_DEBUGGER="node /path/to/launchDebugger.js --port 2345 --type ReactNative"` гээд дараа нь `node /path/to/launchDebugger.js --port 2345 --type ReactNative /path/to/reactNative/app` гэсэн команд өгнө.

> Энэ маягаар хийгдсэн тусгай алдаа засагчийн команд нь богино хугацааных байх ёстой бөгөөд гаралт нь 200 килобайтаас илүүгүй байх хэрэгтэй. 

## Safari Developer Tools

Та аппынхаа iOS хувилбарын алдааг засахдаа "Debug JS Remotely"-ыг идэвхжүүлэхгүйгээр Safari ашиглаж болно.

- Safari дотор Develop menu-ыг идэвхжүүлэх: `Preferences → Advanced → Select "Show Develop menu in menu bar"`
- Аппын JSContext-ыг сонгох: `Develop → Simulator → JSContext`
- Safari's Web Inspector нээгдэнэ. Энэ нь консол болон алдаа засагчтай. 

Гэхдээ хэдэн сул тал бий:

1. Алдаа засах үед эх байршлыг нь заадаггүй.
2. Апп дахин ачаалах үед (live reload ашиглах эсвэл гар аргаар ачаалах) JSContext шинээр үүснэ. "Automatically Show Web Inspectors for JSContexts" гэдгийг сонговол сүүлийн JSContext  хувилбарыг сонгох шаардлагагүй болно.
## React Developer Tools

Та [React Developer Tools-ын бие даасан хувилбар](https://github.com/facebook/react-devtools/tree/master/packages/react-devtools)-ыг ашиглан React компонентийн шатлалын алдааг засаж болно. Ашиглахын тулд `react-devtools` багцыг ил суулгана:

```
npm install -g react-devtools
```

Одоо терминалаас `react-devtools` ажиллуулж, бие даасан DevTools аппыг ажиллуулж эхлүүлнэ:

```
react-devtools
```

![React DevTools](/react-native/docs/assets/ReactDevTools.png)

Хэдэн секундийн дотор симулятортай холбогдоно.

> Тэмдэглэл: хэрэв та ил суулгахыг хүсэхгүй байгаа бол `react-devtools`-ыг харьяа болгон нэмэх боломжтой. `react-devtools` багцыг  `npm install --save-dev react-devtools` ашиглан нэмээд тэгээд `package.json` доторх `scripts` хэсэгт `"react-devtools": "react-devtools"` нэмнэ.  DevTools-ээ нээхийн тулд өөрийн фолдероос `npm run react-devtools` гэснийг ажиллуулна.

### React Native Inspector-тэй нэгтгэх

Апп доторх хөгжүүлэгчийн цэсийг нээн "Toggle Inspector" гэснийг сонгоно. Ингэснээр давхар цонх үүсч та хэрэглэгчийн интерфэйсийн хүссэн элемент руу орж, мэдээлэл харах боломжтой:

![React Native Inspector](/react-native/docs/assets/Inspector.gif)

Гэхдээ `react-devtools` ажиллаж байгаа үед Inspector уналтын горимд шилжих бөгөөд DevTools-ыг хэрэглэгчийн гол интерфэйс болгон ашигладаг. Энэ горимд байгаа үед симулятор доторх ямар нэг зүйл дээр дарвал DevTools доторх холбогдох компонентийг гаргаж ирдэг:

![React DevTools Inspector Integration](/react-native/docs/assets/ReactDevToolsInspector.gif)

Энэхүү горимоос гарахын тулд цэс доторх "Toggle Inspector" гэснийг сонгоно.

### Сomponent Instances шалгах

Chrome-д JavaScript-ын алдаа засаж байгаа үед та хөтчийн консол дотор React компонентуудын пропс болон төлөвийг шалгах боломжтой. 

Эхлээд Chrome-ийн алдаа засах зааврыг даган Chrome консолыг нээнэ үү.

Chrome консолын зүүн дээд буланд `debuggerWorker.js` гэсэн байгаа эсэхийг харна уу.  **Энэ алхам их чухал.**

Тэгээд React DevTools дотор React компонент сонгоно. Дээд хэсэг дэх хайлтын хэсгийг ашиглан нэрээр хайн олох боломжтой. Сонгонгуут Chrome консол дотор `$r` гэж гарах бөгөөд та пропс, төлөв, instance-ын тухай мэдээллийг шалгах боломжтой болно. 

![React DevTools Chrome Console Integration](/react-native/docs/assets/ReactDevToolsDollarR.gif)

## Ажиллагааг хянагч

Хөгжүүлэгчийн цэс дотроос "Perf Monitor" гэснийг сонгон ажиллагаанд тулгарсан асуудлыг засахад туслах ажиллагааны давхар цонхыг идэвхжүүлж болно.

<hr style="margin-top:25px; margin-bottom:25px;"/>

#  Ejected аппын алдааг засах 

<div class="banner-crna-ejected" style="margin-top:25px">
  <h3>Projects with Native Code Only</h3>
  <p>
    Үлдсэн хэсэгт <code>react-native init</code> эсвэл <code>expo init</code> эсвэл ejected болсон Create React Native App ашиглан хийсэн апп-д хамаарах мэдээлэл байгааг анхаарна уу.
Ejecting гэж юу болох талаар мэдэхийг хүсвэл Create React Native App repository-ын <a href="https://github.com/react-community/create-react-native-app/blob/master/EJECTING.md" target="_blank">заавар</a>-тай танилцана уу.
  </p>
</div>

## Console logs-т хандах

Апп ажиллаж байх үед та терминал дотор доорх командыг өгч iOS болон Android-ын console logs-ыг гаргаж ирнэ:

```
$ react-native log-ios
$ react-native log-android
```

Мөн та iOS симулятор дотор `Debug → Open System Log...`  гэж орох эсвэл  Android апп төхөөрөмж дээр, эмулятор дээр ажиллаж байх үед терминалд `adb logcat *:S ReactNative:V ReactNativeJS:V`  гэдгийг ажиллуулан орж болно. 

> Хэрэв та Create React Native App эсвэл Expo CLI ашиглаж байгаа бол console logs нь тухайн ижил терминал дээр багцлагч хэлбэрээр харагдаж байгаа. 

## Chrome Developer Tools ашиглан төхөөрөмжийн алдааг засах

> Хэрэв та Create React Native App эсвэл Expo CLI ашиглаж байгаа бол энэ тохиргоо нь аль хэдийн хийгдсэн байна. 

iOS төхөөрөмж дээр [`RCTWebSocketExecutor.m`](https://github.com/facebook/react-native/blob/master/Libraries/WebSocket/RCTWebSocketExecutor.m) гэсэн файлыг нээн компьютерынхоо IP хаягт "localhost"-ыг өөрчилнө. Тэгээд Хөгжүүлэгчийн цэсээс "Debug JS Remotely" гэснийг сонгоно.


USB холбогдсон Android 5.0+ төхөөрөмж дээр та  [`adb` command line tool](http://developer.android.com/tools/help/adb.html)-ыг ашиглан уг төхөөрөмжөөс компьютер руугаа шилжүүлэх тохиргоог хийж болно:
`adb reverse tcp:8081 tcp:8081`

Эсвэл Хөгжүүлэгчийн цэсээс "Dev Settings" гэдгийг сонгон өөрийн компьютерын  IP хаягтай адилхан байхаар "Debug server host for device" гэдгийг тохируулна. 

> Хэрэв ямар нэг асуудал гарвал Chrome өргөтгөлийн аль нэг нь алдаа засагчид тодорхой бус шалтгаанаар нөлөөлөөд байх боломжтой. Бүх өргөтгөлүүдээ идэвхгүй болгож байгаад асуудалтай байгаа өргөтгөлийг олох хүртэл нэг нэгээр нь идэвхжүүлээрэй. 

## Натив кодын алдааг засах

Натив модуль бичих гэхчлэн натив кодтой ажиллаж байгаа үед та Android Studio эсвэл  Xcode-оос аппаа эхлүүлэн, натив апп хэрхэн хийдэг шигээ хийгээд натив алдаа засагчийг ашиглах боломжтой (зогсоох үеийг тохируулах г.м).
