---
id: building-for-apple-tv
title: Building For TV Devices
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
  .display-platform-ios .toggler .button-ios,
  .display-platform-android .toggler .button-android {
    background-color: #05A5D1;
    color: white;
  }
  block { display: none; }
  .display-platform-ios .ios,
  .display-platform-android .android {
    display: block;
  }
</style> 

React Native аппликейшныг Apple TV болон Android TV дээр ажиллуулах зорилгоор TV төхөөрөмж дэмждэг болгосон байгаа. Тухайн аппликейшны Javascript кодонд цөөн өөрчлөлт хийх эсвэл бүр огт өөрчлөхгүйгээр ажиллуулах боломжтой. 

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

<block class="ios" />

RNTester апп нь Apple TV-ыг дэмждэг; tvOS-д зориулж хийхийн тулд `RNTester-tvOS` ашиглана уу.

## Өөрчлөлтийг нэгтгэх

- _Native layer_: React Native Xcode төслүүд нь одоо бүгд '-tvOS' гэсэн стрингээр төгссөн Apple TV файл ажиллуулдаг болсон. 

- _react-native init_: `react-native init`-аар хийгдсэн React Native шинэ төслүүд автоматаар XCode төсөл дотроо Apple TV файлтай байна.  

- _JavaScript layer_: `Platform.ios.js` дээр Apple TV дэмждэг болсон. Та AppleTV дээр код ажиллаж байгаа эсэхийг доорх маягаар шалгана: 

```javascript
var Platform = require('Platform');
var running_on_tv = Platform.isTV;

// If you want to be more specific and only detect devices running tvOS
// (but no Android TV devices) you can use:
var running_on_apple_tv = Platform.isTVOS;
```

<block class="android" />

## Өөрчлөлтийг нэгтгэх 

- _Native layer_: Android TV дээр React Native төслийг ажиллуулахын тулд `AndroidManifest.xml` дээр доорх өөрчлөлтийг хийнэ үү. 

```xml
  <!-- Add custom banner image to display as Android TV launcher icon -->
 <application
  ...
  android:banner="@drawable/tv_banner"
  >
    ...
    <intent-filter>
      ...
      <!-- Needed to properly create a launch intent when running on Android TV -->
      <category android:name="android.intent.category.LEANBACK_LAUNCHER"/>
    </intent-filter>
    ...
  </application>
```

- _JavaScript layer_: `Platform.android.js` нь Android TV дэмждэг болсон. Код нь Android TV дээр ажиллаж байгаа эсэхийг шалгахын тулд:

```js
var Platform = require('Platform');
var running_on_android_tv = Platform.isTV;
```

<block class="ios android" />

## Код өөрчлөлт

<block class="ios" />

- _General support for tvOS_:Apple TV-ын натив код дахь тодорхой өөрчлөлтүүд нь TARGET_OS_TV-т байгаа. Үүнд tvOS дэмждэггүй API-уудыг хязгаарласан өөрчлөлтүүд (вэб харагдац, слайдерууд, switches, статус цонх г.м) болон TV удирдлага, гар товчлуур дээрээс оруулсан хэрэглэгчийн мэдээлэл дэх өөрчлөлтүүд багтана. 

- _Common codebase_: tvOS, iOS-уудын Objective-C болон JavaScript ихэнх код адилхан байдаг тул iOS-ын докууд tvOS-тай адилхан байна. 

- _Access to touchable controls_: Apple TV дээр натив харагдацын класс нь `RCTTVView` байна. Энэ нь tvOS-ын фокус төхөөрөмжийг ашиглах нэмэлт аргачлалтай. `Touchable`-т фокусын өөрчлөлтийг таних нэмэлт кодтой ба компонентуудын хэв маягыг зөв гаргах бэлэн аргачлалтай. TV удирдлага ашиглан нэг харагдац сонгоход зохих үйлдлийг эхлүүлдэг. Тэгэхээр `TouchableWithoutFeedback`, `TouchableHighlight` болон `TouchableOpacity` нь зүгээр ажиллана. Нарийвчилбал:


  - Дэлгэцэнд хүрэх хөдөлгөөнтэй харагдацад фокуслах бол `onFocus` ашиглана
  - Дэлгэцэнд хүрэх хөдөлгөөнтэй харагдацад фокусгүй болвол `onBlur` ашиглана
  - TV удирдлага дээр "сонгох" товчийг даран дэлгэцэнд хүрэх хөдөлгөөн бүхий харагдац сонгохдоо `onPress`-ыг ашиглана
<block class="android" />

- _Access to touchable controls_: Android TV дээр ажиллах үед Android framework нь автоматаар таны харагдац дээр фокус хийх элементүүдийн байрлалыг харгалзан навигаци хийх чиглэлийг тодорхойлдог. `Touchable` mixin нь фокус өөрчлөлтийг таних, компонентын хэв маягийг зөв гаргах, TV удирдлага ашиглан аливаа харагдацыг сонгох үед зохих үйлдлийг хийнэ. Тэгэхээр `TouchableWithoutFeedback`, `TouchableHighlight`, `TouchableOpacity` болон `TouchableNativeFeedback` нь зүгээр ажиллана. Нарийвчилбал: 

  - Дэлгэцэнд хүрэх хөдөлгөөнтэй харагдацад фокуслах бол `onFocus` ашиглана
  - Дэлгэцэнд хүрэх хөдөлгөөнтэй харагдацад фокусгүй болбол `onBlur` ашиглана
  - TV удирдлага дээр "сонгох" товчийг даран дэлгэцэнд хүрэх хөдөлгөөн бүхий харагдац сонгохдоо `onPress`-ыг ашиглана

<block class="ios" />

- _TV remote/keyboard input_: `RCTTVRemoteHandler` гэсэн шинэ натив класс нь TV удирдлагын үйлдэл танигчийг тохируулдаг. TV удирдлагад үйлдэл хийгдэх үед энэхүү класс нь `RCTTVNavigationEventEmitter`-ын хүлээн авсан сонордуулгыг харуулна (`RCTEventEmitter`-ын дэд класс). Энэ нь JS эвентийг үүсгэнэ. Энэхүү эвентийг `TVEventHandler` JavaScript object хүлээн авна. TV удирдлагын үйлдлийг зохицуулах аппликейшны код нь `TVEventHandler`-ын инстансийг үүсгэх ба доорх кодны дагуу үйлдлийг хүлээн авдаг. TV удирдлагын үйлдлийг зохицуулах аппликейшны код нь `TVEventHandler`-ын инстансийг үүсгэх ба доорх кодны дагуу үйлдлийг хүлээн авдаг: 

<block class="android">

- _TV remote/keyboard input_: `ReactAndroidTVRootViewHelper` гэх шинэ натив класс нь TV удирдлагын үйлдлийг зохицуулагчийг тохируулдаг. TV удирдлагад шинэ үйлдэл хийгдэх үед уг класс нь JS event үүсгэдэг. Энэхүү эвентийг `TVEventHandler` JavaScript объектын инстанс хүлээн авна. TV удирдлагын үйлдлийг зохицуулах аппликейшны код нь `TVEventHandler`-ын инстансийг үүсгэх ба доорх кодны дагуу үйлдлийг хүлээн авдаг:

<block class="ios android">

```javascript
var TVEventHandler = require('TVEventHandler');

class Game2048 extends React.Component {
  _tvEventHandler: any;

  _enableTVEventHandler() {
    this._tvEventHandler = new TVEventHandler();
    this._tvEventHandler.enable(this, function(cmp, evt) {
      if (evt && evt.eventType === 'right') {
        cmp.setState({board: cmp.state.board.move(2)});
      } else if(evt && evt.eventType === 'up') {
        cmp.setState({board: cmp.state.board.move(1)});
      } else if(evt && evt.eventType === 'left') {
        cmp.setState({board: cmp.state.board.move(0)});
      } else if(evt && evt.eventType === 'down') {
        cmp.setState({board: cmp.state.board.move(3)});
      } else if(evt && evt.eventType === 'playPause') {
        cmp.restartGame();
      }
    });
  }

  _disableTVEventHandler() {
    if (this._tvEventHandler) {
      this._tvEventHandler.disable();
      delete this._tvEventHandler;
    }
  }

  componentDidMount() {
    this._enableTVEventHandler();
  }

  componentWillUnmount() {
    this._disableTVEventHandler();
  }
```

<block class="ios" />

- _Dev Menu support_: Симулятор дээр cmd-D нь iOS дээрх шиг хөгжүүлэгчийн цэсийг гаргаж ирнэ. Жинхэнэ Apple TV төхөөрөмжийг гаргахын тулд удирдлага дээр тоглуулах/зогсоох товчийг удаан дарах хэрэгтэй. (Apple TV төхөөрөмжийг сэгсрээд хэрэггүй. Энэ нь ямар ч үр дүнгүй) 


- _TV remote animations_: `RCTTVView` натив код нь хэрэглэгч өөр өөр харагдацыг гаргах гүйлгэх үед нүдийг чиглүүлэх Apple-аас санал болгодог parallax анимейшныг ажиллуулдаг. Анимейшныг идэвхгүй болгох эсвэл өөрчлөх боломжтой. 

- _Back navigation with the TV remote menu button_: `BackHandler` компонент нь Android-ын буцах товчийг дэмжих зорилготой байсан бол одоо TV удирдлагын цэсний товчийг ашиглан Apple TV  дээр навигаци хийх боломжтой болсон. 


- _TabBarIOS behavior_: `TabBarIOS` компонент нь натив `UITabBar` API-ыг ажиллуулдаг ба энэ Apple TV дээр арай өөр байдаг. tvOS дээр таб-ыг дахин рендэр хийхэд төвөг гарахаас сэргийлэхийн тулд ([асуудал](https://github.com/facebook/react-native/issues/15081) гэснийг уншина уу) сонгосон таб дээр зүйл нь анхны рендэр хийх Javascript-ээр тодорхойлогддог бөгөөд хэрэглэгч натив код ашигласны дараа удирддаг болгож болно. 

<block class="android" />

- _Dev Menu support_: Симулятор дээр cmd-M  нь Android дээрх шиг хөгжүүлэгчийн цэсийг гаргана. Жинхэнэ Android TV төхөөрөмжийг гаргаж ирэхийн тулд удирдлага дээрх ухраах товчийг удаан дарна. (Apple TV төхөөрөмжийг сэгсрээд хэрэггүй. Энэ нь ямар ч үр дүнгүй) 

<block class="ios" />

- _Known issues_:

  - [ListView scrolling](https://github.com/facebook/react-native/issues/12793). ListView болон ижил төстэй компонент доторх `removeClippedSubviews`-ыг false болгож өөрчилснөөр энэ асуудлыг шийдэх боломжтой. Энэ тухай илүү дэлгэрэнгүй уншихыг хүсвэл  
  [PR](https://github.com/facebook/react-native/pull/12944) гэснийг харна уу. 

<block class="android" />

- _Known issues_:

  - `InputText` компонент нь одоогоор ажиллахгүй байгаа (фокус хүлээн авахгүй).

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
    }
  }
  convertBlocks();
  guessPlatformAndOS();
</script>
