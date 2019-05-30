---

id: accessibility

title: Хүртээмж

---



## Натив аппын хүртээмж (iOS and Android)



iOS, Android аль аль нь аппыг хөгжлийн бэрхшээлтэй хүмүүс ашиглах боломжийг олгодог API-тай байдаг. Мөн хараагүй хүмүүст зориулсан iOS дээр VoiceOver, Android дээр API гэх дэлгэц дээрхийг уншигч гэх мэт технологитой. Энэ мэтчилэн React Native-т байх аппыг илүү хүртээмжтэй болгох зорилготой API-уудыг хөгжүүлэгчид ашиглаж болно. iOS, Android хоёр бага зэрэг өөр байдаг тул тухайн платформоос шалтгаалан React Native-ын ажиллагаа нь ялгаатай гэдгийг анхаарна уу. 



Та мөн [энэхүү блогийн нийтлэлээс](https://code.facebook.com/posts/435862739941212/making-react-native-apps-accessible/) React Native-ийн хүртээмжийн талаар мэдээлэл авах боломжтой. 



## Аппыг хүртээмжтэй болгох



### Хүртээмжийн онцлог



#### Хүртээмж (iOS, Android)



`true` гэдэг нь харагдац нь хүртээмжтэй элемент гэдгийг илтгэж байгаа юм. Харагдац нь хүртээмжтэй элемент мөн бол энэ нь children-ээ нэг компонентод хамааруулдаг. Анхны тохиргоогоор бол дарж болох бүх элемент нь хүртээмжтэйд тооцогддог.



Android дээр `accessible={true}` react-native-ын Харагдац (View) нь `focusable={true}` гэсэн байдаг.



```javascript

<View accessible={true}>

  <Text>text one</Text>

  <Text>text two</Text>

</View>

```



Дээрх жишээ дээр бид 'text one' болон 'text two' гэсэн дээр хүртээмжийг тусад нь авч үзэх боломжгүй. Оронд нь бид хүртээмжтэй шинж бүхий эцгийнх нь харагдацыг онцолж үзнэ.





#### accessibilityLabel (iOS, Android)



Харагдац нь хүртээмжтэй гэж тэмдэглэгдсэн бол accessibilityLabel ашиглах нь зүйтэй. Тэгвэл VoiceOver ашигладаг хүмүүс ямар элемент сонгосноо мэдэх боломжтой болох юм. Хэрэглэгч тухай элементийг сонгох үед VoiceOver уншиж өгнө.



Ингэхийн тулд View, Text эсвэл Touchable дээрээ `accessibilityLabel`-ыг тохируулж өгөх хэрэгтэй:



```javascript

<TouchableOpacity

  accessible={true}

  accessibilityLabel="Tap me!"

  onPress={this._onPress}>

  <View style={styles.button}>

    <Text style={styles.buttonText}>Press me!</Text>

  </View>

</TouchableOpacity>

```



Дээрх жишээ дээр TouchableOpacity элемент дээр `accessibilityLabel` нь цаанаасаа "Press me!" гэж байхаар бичсэн байна. Тэмдэглэгээ нь зайгаар тусгаарлагдсан текстийг нийлүүлэн гарсан үг юм.



#### accessibilityHint (iOS, Android)



Хүртээмжийн тухай тэмдэглэгээнээс ямар үр дүнд хүрэх гэсэн нь тодорхой биш байх үед хүртээмжтэй холбоотой ямар нэг үйлдэл хийх үед accessibility hint тус болдог. 



Ингэхийн тулд View, Text эсвэл Touchable дээрээ `accessibilityHint`-ыг тохируулж өгнө:



```javascript

<TouchableOpacity

  accessible={true}

  accessibilityLabel="Go back"

  accessibilityHint="Navigates to the previous screen"

  onPress={this._onPress}>

  <View style={styles.button}>

    <Text style={styles.buttonText}>Back</Text>

  </View>

</TouchableOpacity>

```



Дээрх жишээнд iOS дээр хэрэглэгч VoiceOver-ыг идэвхжүүлсэн бол тухайн hint буюу санал зөвлөгөө нь юу гэж байгааг уншиж өгнө. accessibilityHint-тэй холбоотой нэмэлт мэдээллийг [iOS Хөгжүүлэгчийн Док](https://developer.apple.com/documentation/objectivec/nsobject/1615093-accessibilityhint)-оос уншаарай.



Дээрх жишээнд Android хэрэглэгчид Talkback нь санал зөвлөгөөг уншиж өгнө. Одоогоор Android дээр hint өгөх функцийг унтраах боломжгүй байгаа. 



#### accessibilityIgnoresInvertColors(iOS)



Гэрэлд хэт мэдрэг хүмүүсийн нүдэнд таатай байлгах үүднээс дэлгэцийн өнгийг өөрчилдөг функц Accessibility дотор байдаг. Энэ нь ялгадаггүй хүмүүст болон хараа муутай хүмүүст таатай байдаг. Гэхдээ та зураг гэх мэт зүйлийн өнгийг та өөрчлөхийг хүсэхгүй байж болно. Энэ үед та тухайн харагдацад өнгийг нь өөрчлөхгүй гэсэн тохиргоог хийж өгөх боломжтой.



#### accessibilityRole (iOS, Android)



Accessibility Role нь iOS-ын VoiceOver эсвэл Android-ын TalkBack ашиглаж байгаа хүнд ямар төрлийн элемент ашиглаж байгааг нь хэлж өгдөг. Ашиглахын тулд доорхоос хүсс`accessibilityRole`-ыг нь тохируулж:



- **none** Тухайн элемент ямар нэг үүрэггүй бол ашиглана.

- **button** Тухайн элементийг товч гэж үзэх бол ашиглана. 

- **link** Тухайн элементийг холбоос гэж үзэх бол ашиглана. 

- **search** Текс хэсгийн элементийг хайлтын хэсэг гэж үзэх бол ашиглана.

- **image** Тухайн элементийг зураг гэж үзвэл ашиглана. Товч эсвэл холбоостой хослуулан ашиглах боломжтой.

- **keyboardkey** Тухайн элемент keyboard товч шиг ажиллах бол ашиглана. 

- **text** Тухайн элементийг өөрчлөлт оруулах боломжгүй байнгын текст гэж үзвэл ашиглана. 

- **adjustable** Аливаа элементэд "өөрчлөлт"(слайдер г.м) оруулах боломжтой бол ашиглана.

- **imagebutton** Тухайн элементийг товч болон зураг гэж үзэх бол ашиглана.

- **header** Аливаа элемент контент хэсгийн толгой болж байвал ашиглана (навигацийн гарчиг г.м)

- **summary** Аливаа элемент апп нээгдэн ажиллах үед одоогийн нөхцөлийн талаар товч мэдээлэл өгөх зорилгоор ашиглана.



#### accessibilityStates (iOS, Android)



Accessibility State нь  iOS дээр VoiceOver эсвэл Android дээр TalkBack ашиглан одоогийн ашиглаж буй элементийн төлөвийг хэлж өгдөг. Элементийн төлөвийг `selected`, `disabled` эсвэл хоёуланг дээр нь тохируулж болно:



- **selected** Элемент тухайн сонгогдсон төлөвт байгаа үед ашиглана. Жишээ нь нэг товчийг дарж сонгох.

- **disabled** Элементийг идэвхгүй болгосон, хэрэглэж болохгүй үед ашиглана. 



Ашиглахын тулд `selected`, `disabled` эсвэл хоёуланг дээр нь тохируулсан гэснийг агуулсан массивт `accessibilityStates`  гэж тохируулна. 



#### accessibilityViewIsModal (iOS)



Хүлээн авагчаас хамааралтай харагдац доторх тухайн элементүүдийг VoiceOver үл хэрэгсэх эсэхийг бүүлийн итгэ илэрхийлдэг.

Жишээ нь, `A` болн `B` гэсэн хамаарал бүхий хоёрыг агуулсан цонхонд `accessibilityViewIsModal`  нь `B`  харагдац дээр `true` гэж тохируулсанаар VoiceOver нь `A` харагдац доторх элементийг тоохгүй орхих юм. Нөгөө талаас `B`  харагдац нь `C` гэсэн  child харагдацтай бол та `accessibilityViewIsModal`-ыг `C` харагдац дээр `true` гэж тохируулна. VoiceOver  нь `A` харагдац доторх элементийг тоохгүй орхино гэж байдаггүй. 



#### accessibilityElementsHidden (iOS)



Уг хүртээмжийн элементийг хүртээмжийн элементүүд агуулагдсан эсэхийг илэрхийлж буй бүүлийн утга нь далд байна. 

Жишээ нь, хоорондоо хамаарал бүхий `A`, `B` харагдацыг агуулсан цонхонд `B` харагдац дээр `accessibilityElementsHidden`-ыг `true`  гэж тохируулснаар `B` харагдац дахь элементүүдийг VoiceOver тоохгүй орхиход хүргэдэг. Android-ын `importantForAccessibility="no-hide-descendants"` ч мөн адил. 



#### onAccessibilityTap (iOS)



Хүртээмжтэй элемент дээр хоёр товшиж идэвхжүүлэхэд онцгой нэг функцийг ажиллуулах бол үүнийг ашиглана. 



#### onMagicTap (iOS)



Хоёр хуруугаараа товших "magic tap" үйлдэл хийж байгаа үед онцгой нэг функцийг дуудаж ажиллуулах бол үүнийг ашиглана. Magic tap функц нь тухайн компонент дээр хэрэглэгчийн хийх боломжтой хамгийн зохимжтой үйлдлийг хийдэг. iPhone дээрх Phone апп дээр magic tap нь утасны дуудлагад ирэхэд хариу өгөх эсвэл ярьж буй дуудлагыг тасалдаг. Хэрэв тухайн сонгосон элементэд `onMagicTap` функц байхгүй бол байгаа харагдацыг олох хүртэл систем нь харагдацын бүх шатлалыг дамжин шалгадаг. 



#### onAccessibilityEscape (iOS)



Хоёр хуруугаараа Z үсэг зурж буй мэтээр "escape" үйлдэл хийж байгаа үед онцгой нэг функцийг дуудаж ажиллуулах бол үүнийг ашиглана. Escape функц нь хэрэглэгчийн интерфэйсийн дараагийнх руу нь буцдаг. Энэ нь юу гэсэн үг вэ гэхээр навигаци хийхдээ дээш, доош шилжих эсвэл modal хэрэглэгчийн интерфэйсийг хаана гэсэн үг. Хэрэв сонгосон элемент нь `onAccessibilityEscape` функцгүй бол байгаа харагдацыг олох хүртэл систем нь харагдацын бүх шатлалыг дамжин шалгадаг эсвэл олох боломжгүй байна гэж харуулдаг. 



#### accessibilityLiveRegion (Android)



Компонентууд динамикаар өөрчлөгдөх үед TalkBack-ыг хэрэглэгчид анхааруулга өгдөг байх нь бидэнд хэрэгтэй. Ингэхийн тулд 

‘accessibilityLiveRegion’ ашиглана.   ‘none’, ‘polite’ болон ‘assertive’ гэж тохируулах боломжтой:



- **none** Энэхүү харагдац дээр хийсэн өөрчлөлтийн тухай мэдээлэхгүй. 

- **polite** Энэхүү харагдац дээр хийсэн өөрчлөлтийн тухай мэдээлэх хэрэгтэй.

- **assertive** Энэхүү харагдац дээр өөрчлөлт орсон даруйд одоогийн яриаг таслан мэдээлэх хэрэгтэй. 



```javascript

<TouchableWithoutFeedback onPress={this._addOne}>

  <View style={styles.embedded}>

    <Text>Click me</Text>

  </View>

</TouchableWithoutFeedback>

<Text accessibilityLiveRegion="polite">

  Clicked {this.state.count} times

</Text>

```



Дээрх жишээ дээр \_addOne нь state.count  хувьсагчийг өөрчилж байна. Хэрэглэгч TouchableWithoutFeedback дээр дармагц TalkBack Text гэсэн харагдац доторх текстийг уншина.  'accessibilityLiveRegion=”polite”'  байгаа учраас.





#### importantForAccessibility (Android)



Нэг эцэгтэй хоёр UI компонент давхцаад байгаа үед хүртээмжийн хувьд урьдчилан тааварлах боломжгүй нөхцөл байдал үүсэх боломжтой. Харагдац нь accessibility events үүсгэх эсвэл хүртээмжтэй холбоотой үйлчилгээ гэж бүртгэгдсэн тохиолдолд ‘importantForAccessibility’ арга хэмжээ авч үүнийг зохицуулдаг. ‘auto’, ‘yes’, ‘no’ , ‘no-hide-descendants’ гэж тохируулах боломжтой (сүүлийн утга нь хүртээмжийн үйлчилгээ уг компонентыг бол бүх children-ийг тоохгүй орхиход хүргэнэ.



```javascript

<View style={styles.container}>

  <View style={{position: 'absolute', left: 10, top: 10, right: 10, height: 100,

    backgroundColor: 'green'}} importantForAccessibility=”yes”>

    <Text> First layout </Text>

  </View>

  <View style={{position: 'absolute', left: 10, top: 10, right: 10, height: 100,

    backgroundColor: 'yellow'}} importantForAccessibility=”no-hide-descendants”>

    <Text> Second layout </Text>

  </View>

</View>

```



Дээрх жишээ дээр шар layout болон түүний дагаврууд нь TalkBack болон бусад хүртээмжтэй холбоотой үйлчилгээнд огт харагдахгүй. 

Тийм болохоор бид TalkBack-т эргэлзээ үүсгэхгүйгээр ижил эцэгтэй харагдацуудыг давхар ашиглаж болно. 



### Дэлгэц уншигчийг идэвхжүүлсэн эсэхийг шалгах



`AccessibilityInfo` API нь дэлгэц уншигч идэвхтэй байгаа эсэхийг шалгахад тусалдаг.  Дэлгэрэнгүй мэдээллийг [AccessibilityInfo documentation](accessibilityinfo.md)-аас харна уу.



### Accessibility Events илгээх (Android)



Заримдаа accessibility event-ийг UI компонент дээр үүсгэх нь дөхөм байдаг (дэлгэц дээр тусгай харагдац байх эсвэл тусгай радио товчийг сонгосон үед). Native UIManager модуль нь энэ зорилгоор ‘sendAccessibilityEvent’ -ыг ашигладаг. Тааг харах, тухайн event-ийн төрлийг харах гэсэн хоёр сонголттой.



```javascript

import { UIManager, findNodeHandle } from 'react-native';



_onPress: function() {

  const radioButton = this.state.radioButton === 'radiobutton_checked' ?

    'radiobutton_unchecked' : 'radiobutton_checked'



  this.setState({

    radioButton: radioButton

  });



  if (radioButton === 'radiobutton_checked') {

    UIManager.sendAccessibilityEvent(

      findNodeHandle(this),

      UIManager.AccessibilityEventTypes.typeViewClicked);

  }

}



<CustomRadioButton

  accessibilityComponentType={this.state.radioButton}

  onPress={this._onPress}/>

```



Дээрх жишээ дээр бид тусгай радио товчийг үүсгэсэн. Одоо натив шиг ажиллана. Тодруулж хэлбэл TalkBack одооноос радио товчийн сонголтод гарсан өөрчлөлтийг зөв мэдээлэх юм. 



## VoiceOver Support-ыг шалгаж үзэх (iOS)



VoiceOver-ыг идэвхжүүлэхийн тулд iOS төхөөрөмж дээрээ Settings апп руу орж (Симялаторт байхгүй), General гэсэн дээр дараад тэгээд Accessibility гэснийг сонгоно. Тэндээс текс тодруулах, ялгарал сайжруулах, Voiceover гэх мэт хэрэглэгч төхөөрөмжөө илүү сайн ашиглах боломжтой болно.



VoiceOver-ыг идэвхжүүлэхийн тулд  "Vision" гэсний доор VoiceOver гэсэн дээр даран дээр харагдаж буй товчийг чирж идэвхжүүлнэ. 



Accessibility тохиргооны хамгийн доор нь "Accessibility Shortcut" гэж бий. Та Home товч дээр гурав дарахад VoiceOver гарч ирдэг байхыг хүсвэл үүнийг ашиглаарай.



## TalkBack Support-ыг шалгах (Android)



TalkBack-ыг идэвхжүүлэхийн тулд Android төхөөрөмж дээрээ эсвэл эмулятор дээрээ Settings апп руу орно. Accessibility гэсэн дээр дараад TalkBack-ыг сонгоно. Тэгээд "Use service" гэснийг асааж, унтраах маягаар идэвхжүүлэх эсвэл унтраах боломжтой. 



Сануулж хэлэхэд, Android эмулятор нь цаанаасаа TalkBack-тай ирдэггүй. Суулгахын тулд:



1. TalkBack файл эндээс татах: https://google-talkback.en.uptodown.com/android

2. Татсан файлаа эмуляторын `.apk`  файл руу чирэх 



Та TalkBack-ыг ажиллуулахын тулд дуу нэмж хасах товчийг ашиглах боломжтой. Идэвхжүүлэхийн тулд Settings цэс, Accessibility гэж ороод дээд хэсэгт байгаа Volume key shortcut гэснийг идэвхжүүлнэ.



Уг товчийг 3 секунд дарахад accessibilty tools гарч ирнэ.



Хэрэв та хүсвэл command line ашиглан та Talkback-ыг идэвхжүүлэх боломжтой:



```

# disable

adb shell settings put secure enabled_accessibility_services com.android.talkback/com.google.android.marvin.talkback.TalkBackService



# enable

adb shell settings put secure enabled_accessibility_services com.google.android.marvin.talkback/com.google.android.marvin.talkback.TalkBackService

```

