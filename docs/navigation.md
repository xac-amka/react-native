---
id: navigation
title: Дэлгэц хооронд шилжих
---

Ганц нүүр дэлгэцтэй гар утасны апп байх нь ховор. Олон нүүрийг харуулах, хооронд шилжих үйлдэл нь навигатор гэх зүйлээр зохицуулагддаг. 

React Native-т байдаг шилжих үйлдлийн төрөл бүрийн компонентуудын тухай мэдээллийг та эндээс харж болно. Хэрэв та дөнгөж шилжилт хэрхэн хийх тухай судалж эхэлж байгаа бол [React Navigation](navigation.md#react-navigation)-ийг ашиглаж эхлэх байх. React Navigation нь шилжилт хийх процессийг хялбар болгосон ба iOS болон Android дээр түгээмэл ашиглагддаг стекийн шилжилт, таб үүсгэх шилжилтийг хийдэг. 

Хэрэв та iOS, Android аль алин дээр натив харагдуулах эсвэл шилжилтийг натив болгож харагдуулдаг апптай React Native-ыг холбох гэж байгаа бол хоёр платформ дээр натив шилжилт хийхэд энэ сан танд тусална: [react-native-navigation](https://github.com/wix/react-native-navigation).

## React Navigation

Шилжилт хийхэд зориулсан олны оролцоотой нэг шийдэл нь хөгжүүлэгчид цөөн хэдэн мөр код ашиглан дэлгэцүүдийг тохируулах боломжийг олгодог бие даасан сан юм.

Эхний алхам нь суулгах:

```
npm install --save react-navigation
```
Хоёр дахь алхам нь react-native-gesture-handler суулгах:
```
yarn add react-native-gesture-handler
# or with npm
# npm install --save react-native-gesture-handler
```
Одоо бид react-native-ийг react-native-gesture-handler-тай холбох хэрэгтэй

```
react-native link react-native-gesture-handler
```

Тэгээд үндсэн дэлгэц болон профайл дэлгэц бүхий аппыг богино хугацаанд хийх боломжтой:

```javascript
import {createStackNavigator, createAppContainer} from 'react-navigation';

const MainNavigator = createStackNavigator({
  Home: {screen: HomeScreen},
  Profile: {screen: ProfileScreen},
});

const App = createAppContainer(MainNavigator);

export default App;
```

Нүүр бүрийн компонент нь толгой гарчиг гэхчлэн шилжилт хийх сонголтыг тохируулж болдог. `navigation' проп дээрх үйлдэл үүсгэгчийг ашиглан бусад нүүртэй холбож өгдөг:

```javascript
class HomeScreen extends React.Component {
  static navigationOptions = {
    title: 'Welcome',
  };
  render() {
    const {navigate} = this.props.navigation;
    return (
      <Button
        title="Go to Jane's profile"
        onPress={() => navigate('Profile', {name: 'Jane'})}
      />
    );
  }
}
```

React Navigation чиглүүлэгчид нь шилжилт хийх логикийг дахин тодорхойлох явцыг хялбар болгож өгдөг. Чиглүүлэгчид нь нэг нэгнийхээ дотор үүрлэх боломжтой байдаг тул хөгжүүлэгчид өргөн хүрээг хамрахгүйгээр аппын нэг хэсгийн шилжилт хийх логикийг дахин тодорхойлж болдог. 

React Navigation доторх харагдац нь натив компонент болон [`Animated`](animated.md) сан ашиглаж байж натив thread дээр ажиллах 60fps анимейшн гаргадаг. Мөн анимейшн, дохио хөдлөлийг хүссэнээрээ хялбархан өөрчлөх боломжтой.  

React Navigation-ын талаар бүрэн ойлголттой болохыг хүсвэл [React Navigation Getting Started Guide](https://reactnavigation.org/docs/getting-started.html)-ыг унших эсвэл [Intro to Navigators](https://expo.io/@react-navigation/NavigationPlayground) гэх мэт бусад хэсэгтэй танилцаарай. 
