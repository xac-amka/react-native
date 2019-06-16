---
id: direct-manipulation
title: Шууд оролдлого
---

Заримдаа төлөв/пропс ашиглаж дэд модыг /subtree/ бүхэлд нь дахин рендэр хийхгүйгээр компонентод шууд өөрчлөлт хийх нь чухал байдаг. Хөтөч дээр React ашиглаж байгаа үед жишээ нь заримдаа DOM горимд шууд өөрчлөлт оруулах хэрэгтэй болдог ба гар утасны апп дээрх харагдац дээр мөн ийм шаардлага бий болдог.  `setNativeProps` нь DOM node-д тохиргоо хийх боломж олгодог
React Native-ын энэ зэрэгцэхүйц шийдэл юм.

>Дахин дахин рендэр хийсний улмаас ажиллагаа нь тэнцвэргүй болбол setNativeProps-ыг ашиглаарай
> Шууд оролдлого хийх функцийг дахин дахин ашиглаад байх зүйл биш. Рендэр хийж буй компонентын дэс дарааг дарахаас сэргийлэх, олон харагдацыг зохицуулах үед үргэлжилсэн анимейшн бүтээх зорилгоор л ашиглах нь зүйтэй.  `setNativeProps` нь чухал ба  React компонент дотор биш DOM, UIView гэх мэт натив layer-т төлөвийг хадгалдаг. Ингэснээр таны кодоос алдаа шалтаг олоход илүү хэцүү болдог. Хэрэглэхийн өмнө `setState` болон [shouldComponentUpdate](http://facebook.github.io/react/advanced-performance.md#shouldcomponentupdate-in-action) ашиглан гарсан асуудлаа шийдэх гээд оролдоорой. 


## TouchableOpacity ашиглан setNativeProps тохируулах

[TouchableOpacity](https://github.com/facebook/react-native/blob/master/Libraries/Components/Touchable/TouchableOpacity.js) 
нь дотроо `setNativeProps`-ыг ашиглан хүүхэд компонентынхоо бүргэрэлтийн мэдээллийг шинэчилдэг:

```javascript
setOpacityTo(value) {
  // Redacted: animation related code
  this.refs[CHILD_REF].setNativeProps({
    opacity: value
  });
},
```

Ингэснээр ямар нэг шаардлага, өөрчлөлтгүйгээр хүүхэд компонент нь үйлдлээс хамааран өөрийн бүдгэрэлтийн мэдээллээ шинэчилдэг болно:

```javascript
<TouchableOpacity onPress={this._handlePress}>
  <View style={styles.button}>
    <Text>Press me!</Text>
  </View>
</TouchableOpacity>
```

`setNativeProps` байхгүй байлаа гэж төсөөлье. Энэ тохиолдолд өөр нэг арга нь төлөв дотор бүдгэрэлтийн мэдээллийг хадгалан `onPress` ажиллах үед мэдээллийг нь шинэчлэх юм:

```javascript
constructor(props) {
  super(props);
  this.state = { myButtonOpacity: 1, };
}

render() {
  return (
    <TouchableOpacity onPress={() => this.setState({myButtonOpacity: 0.5})}
                      onPressOut={() => this.setState({myButtonOpacity: 1})}>
      <View style={[styles.button, {opacity: this.state.myButtonOpacity}]}>
        <Text>Press me!</Text>
      </View>
    </TouchableOpacity>
  )
}
```

Анхны жишээг бодвол энэ нь тооцоолол ихтэй. Тухайн харагдацын бусад мэдээлэл болон дагавар компонентуудын мэдээлэл өөрчлөгдөөгүй ч гэсэн бүдгэрэлтийн мэдээлэлд өөрчлөлт орох бүрт React дахин рендэр хийх хэрэгтэй болно. Ихэнхдээ энэ тийм сүртэй асуудал биш ч үргэлжилсэн анимейшн үзүүлэх, дохиололд хариу өгөх үед компонентуудаа оновчтой байлгавал чанар нь илүү байх болно.

Хэрэв та [NativeMethodsMixin](https://github.com/facebook/react-native/blob/master/Libraries/Renderer/oss/ReactNativeRenderer-prod.js) дахь `setNativeProps` хэрхэн ажиллаж байгааг харвал `RCTUIManager.updateView`-ын тойронд wrapper буюу хязгаарлагч байгааг анзаарах болно. Энэ нь дахин рендэр хийснээс үүсэх үр дүнтэй адилхан функц юм. [receiveComponent in ReactNativeBaseComponent](https://github.com/facebook/react native/blob/fb2ec1ea47c53c2e7b873acb1cb46192ac74274e/Libraries/Renderer/oss/ReactNativeRenderer-prod.js#L5793-L5813) гэснийг харна уу. 

## Нэгдмэл компонентууд ба setNativeProps

Нэгдмэл компонентууд нь натив харагдацаар баталгааждаггүй учраас `setNativeProps`-ыг нь харж болохгүй. Энэ жишээг хараад үз:

```SnackPlayer name=setNativeProps%20with%20Composite%20Components
import React from 'react';
import { Text, TouchableOpacity, View } from 'react-native';

class MyButton extends React.Component {
  render() {
    return (
      <View>
        <Text>{this.props.label}</Text>
      </View>
    )
  }
}

export default class App extends React.Component {
  render() {
    return (
      <TouchableOpacity>
        <MyButton label="Press me!" />
      </TouchableOpacity>
    )
  }
}
```

Хэрэв үүнийг ажиллуулах юм бол шууд л ийм алдаа заана: `Touchable child must either be native or forward setNativeProps to a native component`. `MyButton` нь бүдгэрлийг нь тохируулсан байх натив харагдацаар шууд баталгаажаагүй учраас тэр. Ингээд ойлгочих: хэрэв та `createReactClass`-тай компонентыг тодорхойлбол үүний хэв маягийнх п пропыгтохируулах хэрэггүй ба ажилладаг байлгах ч хэрэггүй. Та натив компонентыг wrap хийгээгүй л бол хэв маягийн пропыг нь хүүхэд компонентод дамжуулах хэрэгтэй болно. Үүний нэгэн адил бид `setNativeProps`-ыг нативаар баталгаажсан хүүхэд компонент руу илгээнэ.


#### setNativeProps-ыг хүүхэд компонент руу илгээх

Бид ердөө компонент дээрээ  `setNativeProps` аргыг ашиглан холбогдох хүүхэд компонент руу `setNativeProps`-ыг дуудна.

```SnackPlayer name=Forwarding%20setNativeProps
import React from 'react';
import { Text, TouchableOpacity, View } from 'react-native';

class MyButton extends React.Component {
  setNativeProps = (nativeProps) => {
    this._root.setNativeProps(nativeProps);
  }

  render() {
    return (
      <View ref={component => this._root = component} {...this.props}>
        <Text>{this.props.label}</Text>
      </View>
    )
  }
}

export default class App extends React.Component {
  render() {
    return (
      <TouchableOpacity>
        <MyButton label="Press me!" />
      </TouchableOpacity>
    )
  }
}
```

Та одоо `TouchableOpacity` доторх `MyButton` гэснийг ашиглах боломжтой боллоо! Нэмж хэлэхэд бид уламжлалт стринг бүхий холбогч биш, харин [ref callback](https://reactjs.org/docs/refs-and-the-dom.html#adding-a-ref-to-a-dom-element) синтаксийг энд ашигласан байгаа. 

Бид `{...this.props}` ашиглан бүх пропсыг хүүхэд компонент руу дамжуулсныг та анзаарсан байх. `TouchableOpacity` нь нэгдмэл компонент учраас ингэсэн ба хүүхэд компонент дээрх `setNativeProps`-аас хамааралтай учир хүүхэд компонент нь ч бас дэлгэцэнд хүрэх үйлдлийг зохицуулдаг байх шаардлагатай. Ингэхийн тулд `TouchableOpacity` компонентыг дуудах [төрөл бүрийн пропсыг](view.md#onmoveshouldsetresponder) дамжуулдаг. `TouchableHighlight` нь нөгөөтэйгүүр натив харагдацаар баталгааждаг ба `setNativeProps`-ыг л ажиллуулахыг шаарддаг.


##  TextInput-ыг цэвэрлэхийн тулд setNativeProps ашиглах

`setNativeProps` түгээмэл ашиглагддаг өөр нэг тохиолдол нь TextInput дотор оруулсан дүнг арилгах юм.  TextInput-ын `controlled` проп нь заримдаа `bufferDelay` нь бага байгаа үед, мөн хэрэглэгч хэтэрхий хурдан бичих үед үсэг орхих явдал гардаг. Шаардлагатай үед зарим хөгжүүлэгчид энэ пропын оронд `setNativeProps`-ыг ашиглаж TextInput доторх дүнг шууд өөрчлөх гэж оролддог. Жишээ нь доорх код нь нэг товч дээр дарах үед оруулсан дүнг арилгах код юм:

```SnackPlayer name=Clear%20text
import React from 'react';
import { TextInput, Text, TouchableOpacity, View } from 'react-native';

export default class App extends React.Component {
  clearText = () => {
    this._textInput.setNativeProps({text: ''});
  }

  render() {
    return (
      <View style={{flex: 1}}>
        <TextInput
          ref={component => this._textInput = component}
          style={{height: 50, flex: 1, marginHorizontal: 20, borderWidth: 1, borderColor: '#ccc'}}
        />
        <TouchableOpacity onPress={this.clearText}>
          <Text>Clear text</Text>
        </TouchableOpacity>
      </View>
    );
  }
}
```

## Рендэр функцтэй холбоотой аливаа зөрчлөөс зайлсхийх 

Хэрэв та рендэр функцээр зохицуулагддаг зүйлийг шинэчилбэл компонент дахин рендэр эсвэл өөрчлөлт орох бүрт юу нь мэдэгдэхгүй bugs гарч ирэх болно. `setNativeProps`-т өмнө нь оруулсан дүнг огт хэрэгсэхгүй ба шууд л дараад биччихнэ. 

## setNativeProps & shouldComponentUpdate

[`shouldComponentUpdate`-ыг ухаантай ашигласнаар](https://reactjs.org/docs/optimizing-performance.html#avoid-reconciliation) 
та өөрчлөлт ороогүй дэд мод бүхий компонентуудыг нэгтгэхтэй холбоотойгоор `setNativeProps`-ын оронд `setState` ашиглах үед шаардлагагүй зүйлээс зайлсхийх боломжтой. 

## Бусад натив аргууд

Энд дурдсан аргууд нь React Native-т цаанаас нь байдаг ихэнх компонентуудад байдаг. Гэхдээ  натав харагдацаар баталгаажаагүй нэгдмэл компонентууд дээр _байхгүй_ гэдгийг санаарай. Үүнд аппдаа оруулж хийсэн инэнх компонентууд чинь хамаарах болно. 

### хэмжилт(эргэн дуудах)

Аливаа харагдац дахь дэлгэцний байрлал, өргөн, өндрийг тодорхойлох ба тоон дүнг эргэн дуудах замаар гаргадаг. Хэрэв амжилттай болбол доорх маягаар дуудна:


- x
- y
- width
- height
- pageX
- pageY


Натив дотор рендэр хийх процесс дууссаны дараа эдгээр хэмжилт нь харагдана гэдгийг анхаарна уу. Хэрэв та хэмжээсийг тэр дор нь авмаар байвал [`onLayout` prop](view.md#onlayout)-ыг оронд нь ашиглаарай.

### measureInWindow(эргэн дуудах)

Энэ нь тухайн харагдацын дэлгцэц дээрх байршлыг тодорхойлох ба дүнг нь дараа нь эргэн дуудах маягаар харуулдаг. Хэрэв React-ын суурь харагдац нь өөр нэг натив харагдац дотор байвал танд илүү хялбар байх болно. Амжилттай болбол доорх маягаар мэдээллийг харуулна:

- x
- y
- width
- height

### measureLayout(relativeToNativeNode, onSuccess, onFail)


`measure()`-тай адилхан боловч удамшсан зүйлтэй харьцуулж хэмждэг ба `relativeToNativeNode` гэж тодорхойлдог. Эргэн дуудсан x, y  нь удамшсан x, y-тай харьцуулан хэмжигдэнэ гэсэн үг. 

Мөн та компонентын натив node хэлбэрээр авах бол `findNodeHandle(component)` ашиглах боломжтой.

```javascript
import {findNodeHandle} from 'react-native';
```

### фокус()

Аливаа харагдац, оруулсан мэдээллийг тодруулж харуулна. Ямар төрлийн харагдац, ямар платформ гэдгээс хамаарч үйлдэл хийгдэх нь өөр байна.

### бүрсийх()

Аливаа харагдац, оруулсан мэдээллээс фокусыг нь авах үйлдэл. `focus()`-ын эсрэг үйлдэл нь.
