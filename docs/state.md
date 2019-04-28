---
id: state
title: Төлөв
---

Компонентийг удирддаг хоёр төрлийн өгөгдөл байдаг: `props` болон `state`. `props` нь эцэг компонентоос утга оноогдох ба тухайн компонентийг амьдрах хугацаанд оршно. Өөрчлөлт орох өгөгдлийн хувьд бид `state`-ийг ашиглах хэрэгтэй.

Ерөнхийдөө байгуулагч функц дотор `state` -ийг зарлаж, өөрчлөлт хийх бол `setState`-ыг дуудна.

Жишээ нь, текстийг цаг үргэлж анивчдаг болгохыг хүслээ гэж бодъё. Анивчих хэсгийг нь хийчихвэл текстийг нэг л удаа оруулахад болно. Текст нь `prop` нь байх юм. "Текст харагдах, харагдахгүй" төлөвт шилжнэ. Үүнийг нь `state` байлгана гэсэн үг юм.

```ReactNativeWebPlayer
import React, { Component } from 'react';
import { AppRegistry, Text, View } from 'react-native';

class Blink extends Component {
  constructor(props) {
    super(props);
    this.state = { isShowingText: true };

    // 1 секунд тутам төлвийг соль
    setInterval(() => (
      this.setState(previousState => (
        { isShowingText: !previousState.isShowingText }
      ))
    ), 1000);
  }

  render() {
    if (!this.state.isShowingText) {
      return null;
    }

    return (
      <Text>{this.props.text}</Text>
    );
  }
}

export default class BlinkApp extends Component {
  render() {
    return (
      <View>
        <Blink text='Би анивчих дуртай' />
        <Blink text='Анивчих гайхалтай' />
        <Blink text='Ер нь яагаад тэд үүнийг HTML-с авсан юм бэ' />
        <Blink text='Над руу хар над руу хар над руу хар' />
      </View>
    );
  }
}

// Create React Native App ашиглаж байвал доорх мөрийг алгас
AppRegistry.registerComponent('AwesomeProject', () => BlinkApp);
```

Бодит аппликейшн дээр төлвийг цаг хэмжигчээр тохируулахгүй. Серверээс шинэ өгөгдөл авсан эсвэл хэрэглэгч мэдээлэл оруулсан тохиолдолд төлвийг тохируулах хэрэгтэй болно. Мөн та [Redux](https://redux.js.org/) эсвэл [Mobx](https://mobx.js.org/) гэх мэт state container-ууд ашиглаж өгөгдлийн урсгалыг удирдаж болно. Энэ тохиолдолд та шууд `setState` дуудах биш Redux эсвэл Mobx ашиглаж төлвөө өөрчлөх юм.

setState дуудах үед BlinkApp нь компонентоо дахин хэвлэнэ. Цаг хэмжигчинд setState дуудахад компонент нь цаг хэмжигч хөдлөх бүрт дахин хэвлэгдэнэ.

React-д яаж ажилладаг шигээ л төлөв адилхан ажиллана. State-ийн талаар илүү дэлгэрэнгүй мэдээллийг [React.Component API](https://reactjs.org/docs/react-component.html#setstate) эндээс хараарай. Бидний ашиглаж байгаа ихэнх жишээ нь цулгуй хар текстэй, уйтгартай гэж та бодож байгаа байх. Илүү сайхан болгохын тулд та [Style-ийн талаар сураарай](style.md).
