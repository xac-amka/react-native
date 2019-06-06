---
id: height-and-width
title: Өндөр ба өргөн
---

Компонентийн өндөр болон өргөн нь дэлгэц дээрх хэмжээг тодорхойлно.

## Тогтмол хэмжээс

Компонентийн хэмжээсийг тогтоох хамгийн энгийн арга бол тогтмол `width`, `height`-ийг нэмэх юм. React Native доторх бүх хэмжээс нь нэгжгүй байх бөгөөд тусгай нягтралын пикселийг (dips) илэрхийлнэ.

```ReactNativeWebPlayer
import React, { Component } from 'react';
import { AppRegistry, View } from 'react-native';

export default class FixedDimensionsBasics extends Component {
  render() {
    return (
      <View>
        <View style={{width: 50, height: 50, backgroundColor: 'powderblue'}} />
        <View style={{width: 100, height: 100, backgroundColor: 'skyblue'}} />
        <View style={{width: 150, height: 150, backgroundColor: 'steelblue'}} />
      </View>
    );
  }
}

// skip this line if using Create React Native App
AppRegistry.registerComponent('AwesomeProject', () => FixedDimensionsBasics);
```

Энэхүү хэмжээсийг тогтоох аргыг дэлгэцийн хэмжээсээс үл хамааран үргэлж ижил хэмжээст байдаг компонентуудад ашиглах түгээмэл байдаг.

## Уян хатан хэмжээ

Боломжит зайнд сунаж, агшин динамик хөдөлдөг компонентийн хэв маягийг тогтоохдоо `flex` ашиглана. Энгийнээр та `flex: 1`-ийг ашиглахад ижил эхтэй бусад компонентуудын энэ тэнцүү эзэлж байсан боломжит бүх зайг дүүргэнэ. `flex` том өгөх тусам бусад хамаарал бүхий компонентуудтай харьцуулахад эзлэх харьцаа нь илүү өндөр байна.

> Зөвхөн эхийн хэмжээс нь 0-ээс их байвал компонент боломжит зайг дүүргэн сунана. Хэрэв эх нь тогтмол `width` болон `height` эсвэл `flex`-гүй бол эхийн хэмжээс нь 0 байх бөгөөд `flex`-ийн дагаврууд нь үл харагдана.

```ReactNativeWebPlayer
import React, { Component } from 'react';
import { AppRegistry, View } from 'react-native';

export default class FlexDimensionsBasics extends Component {
  render() {
    return (
      // Try removing the `flex: 1` on the parent View.
      // The parent will not have dimensions, so the children can't expand.
      // What if you add `height: 300` instead of `flex: 1`?
      <View style={{flex: 1}}>
        <View style={{flex: 1, backgroundColor: 'powderblue'}} />
        <View style={{flex: 2, backgroundColor: 'skyblue'}} />
        <View style={{flex: 3, backgroundColor: 'steelblue'}} />
      </View>
    );
  }
}

// skip this line if using Create React Native App
AppRegistry.registerComponent('AwesomeProject', () => FlexDimensionsBasics);
```

Компонентийн хэмжээг тогтоосны дараа [дэлгэц дээр хэрхэн гаргах тухай ](flexbox.md) үзээрэй.
