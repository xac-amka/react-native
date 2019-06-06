---
id: improvingux
title: Хэрэглэгчид таатай болгох
---

## Текст оруулах тохиргоо

Жижиг дэлгэцтэй, програмчилсан товчлууртай утсан дээр текс оруулах амаргүй. Хэдий тийм боловч та өөрт шаардлагатай өгөгдлөөс хамаарч текст оруулах явцыг илүү хялбар болгох боломжтой:


- Эхний эгнээ хэсэг дээр шууд төвлөрдөг болгох 
- Оруулж магадгүй хэлбэрийн текстийг урьдчилан байршуулах 
- Автоматаар үг томоор бичих, алдаа засах функцийг идэвхжүүлэх эсвэл унтраах autocorrect
- Товчлуурын төрлийг сонгох (имэйл, тоон г.м)
- Буцах товч нь дараагийн талбар руу шилжих эсвэл форм илгээхээр тохиргоо хийгдсэн эсэхийг анзаарна уу.

Тохиргооны талаар [`TextInput` docs](textinput.md) гэдгээс дэлгэрэнгүй уншина уу.

<video src="/react-native/img/textinput.mp4" muted autoplay loop width="320" height="430"></video>

[Өөрийн утсан дээр хийж үзэх](https://snack.expo.io/H1iGt2vSW)

## Товчлуур харагдаж байгаа үед layout-аа удирдах

Програмчилсан товчлуур нь дэлгэцийн бараг тал зайг эзэлдэг. Хэрэв танд товчлуур ашиглан хийж болох интерактив элемент байгаа бол [`KeyboardAvoidingView` component](keyboardavoidingview.md) ашиглан орж болох эсэхийг шалгаарай.

<video src="/react-native/img/keyboardavoidingview.mp4" muted autoplay loop width="320" height="448"></video>

[Өөрийн утсан дээр хийж үзэх](https://snack.expo.io/ryxRkwnrW)

## Товших хэсгийг илүү том болгох

Гар утсан дээр товчлуур дарж байгаа үед яг онож дарахад хэцүү байдаг. Тийм болохоор интерактив элементүүдээ 44x44 юм у, үүнээс том байхаар хийгээрэй. Үүнийг шийдэх нэг арга бол тухайн элементэд хангалттай зай үлдээх юм. `padding`, `minWidth` болон `minHeight` хэв маягийг ашиглаж болно. Эсвэл [`hitSlop` prop](touchablewithoutfeedback.md#hitslop) ашиглан layout-д нөлөөлөхгүйгээр интерактив хэсгээ нэмж болно. Демо:

<video src="/react-native/img/hitslop.mp4" muted autoplay loop width="320" height="120"></video>

[Өөрийн утсан дээр хийж үзэх](https://snack.expo.io/rJPwCt4HZ)

## Android Ripple ашиглах

Android API 21+ нь хэрэглэгч дэлгэц дээрх интерактив хэсэг дээр хүрэх үед хариу өгдөг дизайнтай  React Native-т [`TouchableNativeFeedback` component](touchablenativefeedback.md) ашиглан үүнийг хийж болно. Бүдгэрэл, тодруулах функцийн оронд энэ эффектийг ашигласнаар апп тань тухайн платформд илүү таарч байгаа мэт санагдана. Ашиглахдаа болгоомжтой хандах хэрэгтэй. iOS болон Android API < 21 дээр ажиллахгүй учир iOS дээрх бусад Touchable компонентууд ашиглаж байгаа бол мэдээллээ хадгалах хэрэгтэй болно. Платформ хоорондын ялгаатай функцийг хэрхэн зохицуулах тухай [react-native-platform-touchable](https://github.com/react-community/react-native-platform-touchable) гэх сангаас уншаарай.

<video src="/react-native/img/ripple.mp4" muted autoplay loop width="320"></video>

[Өөрийн утсан дээр хийж үзэх](https://snack.expo.io/SJywqe3rZ)

## Дэлгэцийн байрлал түгжих

Та `Dimensions` API ашиглаагүй эсвэл дэлгэцийн байрлалыг өөрчилж тохируулаагүй бол дэлгэцийн байрлалыг солигддог байхаар анхнаасаа тохиргоотой байдаг. Хэрэв та байрлал олон солилддог байхыг хүсэхгүй байгаа бол босоо эсвэл хэвтээ чиглэлд байхаар тохируулан түгжих боломжтой. 

iOS дээр General tab-руу орон Xcode-ийн Deployment Info хэсэг рүү орж хүссэн Device Orientation гэдгийг идэвхжүүлнэ (Өөрчлөлт хийх үедээ Төхөөрөмж цэсээс iPhone гэдгийг сонгосон эсэхээ шалгаарай). Android-ын хувьд AndroidManifest.xml файлыг нээгээд үйл ажиллагааны элемент дээр `'android:screenOrientation="portrait"'` гэдгийг нэмж дэлгэцийг босоо хэлбэрээр эсвэл `'android:screenOrientation="landscape"'` гэдгийг нэмж хэвтээ байхаар түгжих боломжтой. 

# Илүү дэлгэрэнгүйг

Гар утасны платформд зориулсан дизайн өөрчлөх тухай [Material Design](https://material.io/) болон [Human Interface Guidelines](https://developer.apple.com/ios/human-interface-guidelines/overview/design-principles/)-аас уншиж болно.
