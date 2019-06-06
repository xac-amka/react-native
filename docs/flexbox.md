---
id: flexbox
title: Layout with Flexbox
---

Компонент нь flexbox алгоритм ашиглан дагавруудынхаа харагдах байдлыг нарийн тодорхойлдог. Flexbox нь өөр өөр дэлгэцийн хэмжээнд тогтсон харагдах зориулалттай.

Та өөрийн хүссэн харагдах байдлыгййййййжооююв бий болгохын тулд `flexDirection`, `alignItems`,`justifyContent` нарыг хослуулан ашиглана.

> Flexbox нь веб дээр CSS-д ажилладагтайгаа ижилхэн React Native дотор ажиллана. Цөөн хэдэн ялгаа бий. Эхний өгөгдмөл нь өөр байдаг. `flexDirection` ашиглахад `row` биш `column`-руу шилжих бөгөөд `flex` параметр нь зөвхөн нэг л тоо байх боломжтой.

#### Flex чилгэл

Компонентийн `style`-д `flexDirection` нэмвэл харагдах төлвийн **анхдагч тэнхлэгийг** тодорхойлдог. Дагаврууд нь хөндлөнгөөр (`row`) эсвэл босоогоор (`column`) байх уу? Өгөгдмөл тохиргоо нь `column` байх юм.

import React, { Component } from 'react'; import { AppRegistry, View } from 'react-native';

export default class FlexDirectionBasics extends Component { render() { return ( // Try setting `flexDirection` to `column`. <View style={{flex: 1, flexDirection: 'row'}}> <View style={{width: 50, height: 50, backgroundColor: 'powderblue'}} /> <View style={{width: 50, height: 50, backgroundColor: 'skyblue'}} /> <View style={{width: 50, height: 50, backgroundColor: 'steelblue'}} /> </View> ); } };

// skip this line if using Create React Native App AppRegistry.registerComponent('AwesomeProject', () => FlexDirectionBasics);

````

#### Контентийг энэ тэнцүү тараах

Компонентын хэв маяг дээр `justifyContent` гэж нэмвэл дагавруудын **тархалт** нь **анхдагч тэнхлэг** дагуу байна.
Дагаврууд нь эхлэл, төв, төгсгөл хэсэгт байрласан байх уу эсвэл хоорондын зай нь тэгш байх уу? `flex-start`, `center`, `flex-end`, `space-around`, `space-between`, `space-evenly` гэсэн боломжит хувилбарууд байна.

```ReactNativeWebPlayer
import React, { Component } from 'react';
import { AppRegistry, View } from 'react-native';

export default class JustifyContentBasics extends Component {
  render() {
    return (
      // Try setting `justifyContent` to `center`.
      // Try setting `flexDirection` to `row`.
      <View style={{
        flex: 1,
        flexDirection: 'column',
        justifyContent: 'space-between',
      }}>
        <View style={{width: 50, height: 50, backgroundColor: 'powderblue'}} />
        <View style={{width: 50, height: 50, backgroundColor: 'skyblue'}} />
        <View style={{width: 50, height: 50, backgroundColor: 'steelblue'}} />
      </View>
    );
  }
};

// skip this line if using Create React Native App
AppRegistry.registerComponent('AwesomeProject', () => JustifyContentBasics);
````

#### Байрлуулах

Компонентийн хэв маягт `alignItems` нэмснээр дагавруудыг **хоёрдогч тэнхлэг** дагуу **зэрэгцээ байрлал**-д байлгадаг. Хэрэв анхдагч тэнхлэг нь `row` байвал хоёрдогч тэнхлэг нь `column` байна. `column` байвал `row` байна. Дагаврууд нь эхлэл, төв, төсгөл хэсэгт байрлана. Эсвэл дэлгэцийг дүүргэхээр сунаж байрлана. `flex-start`, `center`, `flex-end`, `stretch` гэсэн боломжит хувилбарууд байна.

> `stretch` болгоход дагаврууд нь хоёрдогч тэнхлэгийн дагуу тогтсон хэмжээсгүй байх ёстой. Дараах жишээнээс `alignItems: stretch` гэж тохируулад дагавруудын `width: 50` гэснийг арилгахаас нааш ямар ч өөрчлөлт орохгүй байгааг харж болно.

```ReactNativeWebPlayer
import React, { Component } from 'react';
import { AppRegistry, View } from 'react-native';

export default class AlignItemsBasics extends Component {
  render() {
    return (
      // Try setting `alignItems` to 'flex-start'
      // Try setting `justifyContent` to `flex-end`.
      // Try setting `flexDirection` to `row`.
      <View style={{
        flex: 1,
        flexDirection: 'column',
        justifyContent: 'center',
        alignItems: 'stretch',
      }}>
        <View style={{width: 50, height: 50, backgroundColor: 'powderblue'}} />
        <View style={{height: 50, backgroundColor: 'skyblue'}} />
        <View style={{height: 100, backgroundColor: 'steelblue'}} />
      </View>
    );
  }
};

// skip this line if using Create React Native App
AppRegistry.registerComponent('AwesomeProject', () => AlignItemsBasics);
```

#### Илүү ихийг судлах

Бид үндсэн ойлголттой боллоо. Харагдах байдлыг тодорхойлох өөр олон хэв маяг байдаг. Харагдах байдлыг удирддаг пропсийн бүрэн жагсаалтыг [эндээс](./layout-props.md) харна уу.

Бид жинхэнэ аппликейшн хийж чаддаг болоход тун ойрхон байна. Одоо дутуу байгаа нэг зүйл нь хэрэглэгчийн оруулсан мэдээллийг хэрхэн авах вэ гэдэг байна. Тиймээс [Текст оруулах компонентийг ашиглан текст хэрхэн оруулах вэ](handling-text-input.md) гэдгийг сурцгаая.
