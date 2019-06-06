---
id: components-and-apis
title: Компонент ба API
---

React Native-т өөрийнх нь хэд хэдэн компонент байдаг. Дэлгэцийн зүүн гар талаас та компонент болон API-ийн бүрэн жагсаалтыг харж болно. Хэрэв хаанаас эхлэхээ мэдэхгүй бол доорх ангилсан хэсгүүдийг нэг хараарай:

- [Үндсэн компонентүүд](components-and-apis.md#basic-components)
- [Хэрэглэгчийн интерфэйс](components-and-apis.md#user-interface)
- [Жагсаалт харах](components-and-apis.md#list-views)
- [iOS-д зориулсан](components-and-apis.md#ios-components-and-apis)
- [Android-д зориулсан](components-and-apis.md#android-components-and-apis)
- [Бусад](components-and-apis.md#others)

React Native-т өгөгдсөн байх компонент болон API-нуудад заавал баригдах хэрэггүй. React Native бол олон мянган хөгжүүлэгчийн нэгдэл юм. Хэрэв танд ямар нэг зүйл хэрэгтэй байгаад түүнийг агуулсан сан хайж байгаа бол npm бүртгэлээс [react-native](https://www.npmjs.com/search?q=react-native&page=1&ranking=optimal) гэсэн package-ийг хайх эсвэл [Awesome React Native](http://www.awesome-react-native.com/)-ээс цэгцтэй жагсаалтыг хараарай.

## Үндсэн компонент

Ихэнх аппууд эдгээр үндсэн компонентуудаас аль нэгийг ашигласан байдаг. Хэрэв та React Native-ийг дөнгөж ашиглаж эхэлж байгаа бол эдгээрийг нэг бүрчлэн уншиж танилцах нь зүйтэй.

<div class="component-grid component-grid-border">
  <div class="component">
    <h3><a href="view.html">View</a></h3>
    <p>The most fundamental component for building a UI.</p>
  </div>
  <div class="component">
    <h3><a href="text.html">Text</a></h3>
    <p>A component for displaying text.</p>
  </div>
  <div class="component">
    <h3><a href="image.html">Image</a></h3>
    <p>A component for displaying images.</p>
  </div>
  <div class="component">
    <h3><a href="textinput.html">TextInput</a></h3>
    <p>A component for inputting text into the app via a keyboard.</p>
  </div>
  <div class="component">
    <h3><a href="scrollview.html">ScrollView</a></h3>
    <p>Provides a scrolling container that can host multiple components and views.</p>
  </div>
  <div class="component">
    <h3><a href="stylesheet.html">StyleSheet</a></h3>
    <p>Provides an abstraction layer similar to CSS stylesheets.</p>
  </div>
</div>

## Хэрэглэгчийн интерфейс

Доорх компонентуудыг ашиглан ямар ч платформ дээр түгээмэл ашиглагддаг хэрэглэгчийн интерфэйс удирдлагыг үүсгэж болно. Тодорхой платформ дээр ажилладаг компонентийн тухай мэдэхийг хүсвэл цааш үргэлжлүүлэн уншина уу.

<div class="component-grid component-grid-border">
  <div class="component">
    <h3><a href="button.html">Button</a></h3>
    <p>A basic button component for handling touches that should render nicely on any platform.</p>
  </div>
  <div class="component">
    <h3><a href="picker.html">Picker</a></h3>
    <p>Renders the native picker component on iOS and Android.</p>
  </div>
  <div class="component">
    <h3><a href="slider.html">Slider</a></h3>
    <p>A component used to select a single value from a range of values.</p>
  </div>
  <div class="component">
    <h3><a href="switch.html">Switch</a></h3>
    <p>Renders a boolean input.</p>
  </div>
</div>

## Жагсаалт харах

Ерөнхий агуулгатай ScrollView-ийг бодвол доорх жагсаалт нь зөвхөн одоо дэлгэц дээр харагдаж байгаа зүйлсийг л ажиллуулдаг. Тиймээс урт жагсаалт бүхийг өгөгдлийг харуулахад тун тохиромжтой.

<div class="component-grid component-grid-border">
  <div class="component">
    <h3><a href="flatlist.html">FlatList</a></h3>
    <p>A component for rendering performant scrollable lists.</p>
  </div>
  <div class="component">
    <h3><a href="sectionlist.html">SectionList</a></h3>
    <p>Like <code>FlatList</code>, but for sectioned lists.</p>
  </div>
</div>

## iOS компонент болон API

Доорх компонентуудын ихэнх нь түгээмэл ашиглагддаг UIKit классуудад зориулсан wrapper-тай байдаг.

<div class="component-grid component-grid-border">
  <div class="component">
    <h3><a href="actionsheetios.html">ActionSheetIOS</a></h3>
    <p>API to display an iOS action sheet or share sheet.</p>
  </div>
  <div class="component">
    <h3><a href="alertios.html">AlertIOS</a></h3>
    <p>Create an iOS alert dialog with a message or create a prompt for user input.</p>
  </div>
  <div class="component">
    <h3><a href="datepickerios.html">DatePickerIOS</a></h3>
    <p>Renders a date/time picker (selector) on iOS.</p>
  </div>
  <div class="component">
    <h3><a href="imagepickerios.html">ImagePickerIOS</a></h3>
    <p>Renders a image picker on iOS.</p>
  </div>
  <div class="component">
    <h3><a href="navigatorios.html">NavigatorIOS</a></h3>
    <p>A wrapper around <code>UINavigationController</code>, enabling you to implement a navigation stack.</p>
  </div>
  <div class="component">
    <h3><a href="progressviewios.html">ProgressViewIOS</a></h3>
    <p>Renders a <code>UIProgressView</a></code> on iOS.</p>
  </div>
  <div class="component">
    <h3><a href="pushnotificationios.html">PushNotificationIOS</a></h3>
    <p>Handle push notifications for your app, including permission handling and icon badge number.</p>
  </div>
  <div class="component">
    <h3><a href="segmentedcontrolios.html">SegmentedControlIOS</a></h3>
    <p>Renders a <code>UISegmentedControl</code> on iOS.</p>
  </div>
  <div class="component">
    <h3><a href="tabbarios.html">TabBarIOS</a></h3>
    <p>Renders a <code>UITabViewController</code> on iOS. Use with <a href="tabbarios-item.html">TabBarIOS.Item</a>.</p>
  </div>
</div>

## Android компонент ба API

Доорх компонентуудын инэнх нь түгээмэл ашиглагддаг Android классуудад зориулсан wrapper-тай байдаг.

<div class="component-grid component-grid-border">
  <div class="component">
    <h3><a href="backhandler.html">BackHandler</a></h3>
    <p>Detect hardware button presses for back navigation.</p>
  </div>
  <div class="component">
    <h3><a href="datepickerandroid.html">DatePickerAndroid</a></h3>
    <p>Opens the standard Android date picker dialog.</p>
  </div>
  <div class="component">
    <h3><a href="drawerlayoutandroid.html">DrawerLayoutAndroid</a></h3>
    <p>Renders a <code>DrawerLayout</code> on Android.</p>
  </div>
  <div class="component">
    <h3><a href="permissionsandroid.html">PermissionsAndroid</a></h3>
    <p>Provides access to the permissions model introduced in Android M.</p>
  </div>
  <div class="component">
    <h3><a href="progressbarandroid.html">ProgressBarAndroid</a></h3>
    <p>Renders a <code>ProgressBar</code> on Android.</p>
  </div>
  <div class="component">
    <h3><a href="timepickerandroid.html">TimePickerAndroid</a></h3>
    <p>Opens the standard Android time picker dialog.</p>
  </div>
  <div class="component">
    <h3><a href="toastandroid.html">ToastAndroid</a></h3>
    <p>Create an Android Toast alert.</p>
  </div>
  <div class="component">
    <h3><a href="toolbarandroid.html">ToolbarAndroid</a></h3>
    <p>Renders a <code>Toolbar</code> on Android.</p>
  </div>
  <div class="component">
    <h3><a href="viewpagerandroid.html">ViewPagerAndroid</a></h3>
    <p>Container that allows to flip left and right between child views.</p>
  </div>
</div>

## Бусад

Тодорхой аппликейшнуудад эдгээр компонентууд хэрэг болно. Компонент болон API-гийн бүрэн жагсаалтыг харах бол дэлгэцийн зүүн хэсгийг харна уу.

<div class="component-grid">
  <div class="component">
    <h3><a href="activityindicator.html">ActivityIndicator</a></h3>
    <p>Displays a circular loading indicator.</p>
  </div>
  <div class="component">
    <h3><a href="alert.html">Alert</a></h3>
    <p>Launches an alert dialog with the specified title and message.</p>
  </div>
  <div class="component">
    <h3><a href="animated.html">Animated</a></h3>
    <p>A library for creating fluid, powerful animations that are easy to build and maintain.</p>
  </div>
  <div class="component">
    <h3><a href="cameraroll.html">CameraRoll</a></h3>
    <p>Provides access to the local camera roll / gallery.</p>
  </div>
  <div class="component">
    <h3><a href="clipboard.html">Clipboard</a></h3>
    <p>Provides an interface for setting and getting content from the clipboard on both iOS and Android.</p>
  </div>
  <div class="component">
    <h3><a href="dimensions.html">Dimensions</a></h3>
    <p>Provides an interface for getting device dimensions.</p>
  </div>
  <div class="component">
    <h3><a href="keyboardavoidingview.html">KeyboardAvoidingView</a></h3>
    <p>Provides a view that moves out of the way of the virtual keyboard automatically.</p>
  </div>
  <div class="component">
    <h3><a href="linking.html">Linking</a></h3>
    <p>Provides a general interface to interact with both incoming and outgoing app links.</p>
  </div>
  <div class="component">
    <h3><a href="modal.html">Modal</a></h3>
    <p>Provides a simple way to present content above an enclosing view.</p>
  </div>
  <div class="component">
    <h3><a href="pixelratio.html">PixelRatio</a></h3>
    <p>Provides access to the device pixel density.</p>
  </div>
  <div class="component">
    <h3><a href="refreshcontrol.html">RefreshControl</a></h3>
    <p>This component is used inside a <code>ScrollView</code> to add pull to refresh functionality.</p>
  </div>
  <div class="component">
    <h3><a href="statusbar.html">StatusBar</a></h3>
    <p>Component to control the app status bar.</p>
  </div>
  <div class="component">
    <h3><a href="webview.html">WebView</a></h3>
    <p>A component that renders web content in a native view.</p>
  </div>
</div>
