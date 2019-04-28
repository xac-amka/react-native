---
id: props
title: Пропс
---

Ихэнх компонентүүд үүсэхдээ өөр өөр параметрын утга авснаар өөр байх боломжтой болдог. Эдгээр параметрүүдийг `props` гэж нэрлэдэг.

Жишээ нь, React Native-ийн нэг үндсэн компонент бол `Image`. Зураг харуулая гэж бодоход та `source` гэдэг нэртэй проп үүсгэн тухайн зураг юу харуулах гэж буйг удирдаж болно.

```ReactNativeWebPlayer
import React, { Component } from 'react';
import { AppRegistry, Image } from 'react-native';

export default class Bananas extends Component {
  render() {
    let pic = {
      uri: 'https://upload.wikimedia.org/wikipedia/commons/d/de/Bananavarieties.jpg'
    };
    return (
      <Image source={pic} style={{width: 193, height: 110}}/>
    );
  }
}

// Create React Native App ашиглаж байвал доорх мөрийг алгас
AppRegistry.registerComponent('AwesomeProject', () => Bananas);
```

`{pic}` гэсэн нь хаалтанд байгааг анзаарна уу – `pic` хувьсагчийг JSX руу оруулсан байгаа. Та JavaScript-ийн ямар ч илэрхийллийг JSX-т хаалтанд хийж болно.

Таны өөрийн оруулсан компонент нь `props` байж болно. Ингэснээр танд нэг компонентийг аппынхаа олон газарт ашиглах боломж олгоно. Ингэхдээ ашигласан газар бүртээ арай өөр пропстой ашиглаж болно. `render` функц дотроо `this.props` гэснийг ашиглахад болно. Жишээ нь:

```ReactNativeWebPlayer
import React, { Component } from 'react';
import { AppRegistry, Text, View } from 'react-native';

class Greeting extends Component {
  render() {
    return (
      <View style={{alignItems: 'center'}}>
        <Text>Hello {this.props.name}!</Text>
      </View>
    );
  }
}

export default class LotsOfGreetings extends Component {
  render() {
    return (
      <View style={{alignItems: 'center', top: 50}}>
        <Greeting name='Rexxar' />
        <Greeting name='Jaina' />
        <Greeting name='Valeera' />
      </View>
    );
  }
}

// Create React Native App ашиглаж байвал доорх мөрийг алгас
AppRegistry.registerComponent('AwesomeProject', () => LotsOfGreetings);
```

`name`-ийг проп болгосноор `Greeting` компонентийг өөрчлөх боломжтой болгож байна. Тэгэхээр бид энэ компонентийг мэндчилгээ тус бүртээ дахин ашиглаж болно. Энэхүү жишээн дээр төрөлх компонент мэтээр JSX-д `Greeting` хэсгийг ашигласан байна. Үүнийг хийх боломж нь React-ийг илүү догь болгож байгаа юм. Хэрэв та хэрэглэгчтэй харилцах интерфейсээ өөрчлөхийг хүсвэл өөрөө шинээр зохион гаргаж болно.

Өөр нэг зүйл нь [`View`](view.md) компонент юм. [`View`](view.md) нь бусад компонентүүдийг агуулах компонент болгон ашиглах давуу талтай бөгөөд style болон layout-ийг удирдахад тусалдаг.

`props` болон [`Text`](text.md), [`Image`](image.md), ба [`View`](view.md) компонентүүдийн тусламжтай та олон төрлийн статик дэлгэц хийх боломжтой. Аппаа хэрхэн өөрчлөгддөг байхаар хийх тухай мэдэхийг хүсвэл [State-ын тухай уншаарай](state.md).
