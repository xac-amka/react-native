---
id: animations
title: Анимейшн 
---

Анемейшн нь хэрэглэгчийн сэтгэл хүрч чаддаг. Хөдөлгөөнгүй зүйлс хөдөлж эхлэхэд нэгэн хэвийн байдал арилдаг. Хөдөлж байгаа зүйлс өөрийн гэсэн хэмнэлтэй байх бөгөөд гэнэт шууд зогсчихдоггүй. Анимейшны тусламжтай та итгэл төрөх, жинхэнэ мэт хэмнэлийг бий болгох боломжтой.

React Native-т хоёр төрлийн нэмэлт анимейшн систем байдаг. [`Animated`](animations.md#animated-api) нь нарийн ширхэгтэй, онцгой тэмдэгтийн интерактив удирдлага бүхий систем бол [`LayoutAnimation`](animations.md#layoutanimation-api) нь хөдөлгөөнт global layout-тай.

## `Animated` API

[`Animated`](animated.md) API нь олон төрлийн сонирхолтой анимейшныг маш хялбархнаар товч тодорхой харуулах зорилготой бөгөөд харилцан үйлчлэл нь их сайн ажиллаж чаддаг. `Animated` оролт, гаралтын харилцааг сайтар тусгаж, хоорондын шилжилтийг тохируулдаг ба хугацаа заасан анимейшныг удирдах `start`/`stop` гэсэн энгийн хэрэглүүртэй.

`Animated` нь  `View`, `Text`, `Image`, `ScrollView` гэсэн дөрвөн төрлийн хөдөлгөөнд оруулж болох компонентуудыг экспорт хийдэг. Гэхдээ та  `Animated.createAnimatedComponent()` ашиглан өөрөө бас хийх боломжтой.

Жишээ нь, контейнерт хандах үед уусан алга болдог байхаар хийвэл үүн шиг харагдана:

```SnackPlayer
import React from 'react';
import { Animated, Text, View } from 'react-native';

class FadeInView extends React.Component {
  state = {
    fadeAnim: new Animated.Value(0),  // Initial value for opacity: 0
  }

  componentDidMount() {
    Animated.timing(                  // Animate over time
      this.state.fadeAnim,            // The animated value to drive
      {
        toValue: 1,                   // Animate to opacity: 1 (opaque)
        duration: 10000,              // Make it take a while
      }
    ).start();                        // Starts the animation
  }

  render() {
    let { fadeAnim } = this.state;

    return (
      <Animated.View                 // Special animatable View
        style={{
          ...this.props.style,
          opacity: fadeAnim,         // Bind opacity to animated value
        }}
      >
        {this.props.children}
      </Animated.View>
    );
  }
}

// You can then use your `FadeInView` in place of a `View` in your components:
export default class App extends React.Component {
  render() {
    return (
      <View style={{flex: 1, alignItems: 'center', justifyContent: 'center'}}>
        <FadeInView style={{width: 250, height: 50, backgroundColor: 'powderblue'}}>
          <Text style={{fontSize: 28, textAlign: 'center', margin: 10}}>Fading in</Text>
        </FadeInView>
      </View>
    )
  }
}
```

Энд яг юу болж байгааг дэлгэрэнгүй харъя. `FadeInView` дотор `fadeAnim` нэртэй шинэ  `Animated.Value` үүссэн ба `state`-ын нэг хэсэг болж ажиллаж эхэлсэн байна. `View`-ын бүдгэрлийн хэмжээ нь энэхүү хөдөлгөөнт утгатай холбогдсон байна. Цаанаа бол тоон утга бүдгэрлийн хэмжээг тодорхойлж байгаа.

Компонент дуудах үед бүдгэрэл нь 0 байна. Тэгээд хөдөлгөөнт утга `fadeAnim`дээр анимейшн эхлэх ба утга нь эцэстээ 1 болох хүртэл хамаарал бүхий mapping-уудыг бүгдийг шинэчилнэ (Энэ жишээ дээр бол зөвхөн бүдгэрэл нь).

Энэ арга нь `setState`  дуудаж, дахин рендэр хийснээс хамаагүй хурдан, үр дүнтэй арга юм. Яагаад гэвэл бүх тохиргоо нь ерөнхий байх ба хожим тохиргоогоо цувуулан гаргаж, хамгийн эхэнд анимейшн ажиллуулахад туслахаар тохируулах боломжтой.


### Анимейшны тохиргоо хийх

Анимейшн нь маш нарийн тохиргоо шаарддаг. Хувирах хөдөлгөөнийг өөрийнхөөрөө гаргах,  өмнө нь тохируулах, удаашруулах, хугацаа өгөх, задрах коэффициент (decay factor),  үсрэх тогтмол (spring constant) гэх мэт олон зүйлийг анимейшны төрлөөс хамааран тохируулж болно. 

`Animated` нь хэд хэдэн анимейшны төрөлтэй бөгөөд хамгийн түгээмэл ашиглагддаг нь [`Animated.timing()`](animated.md#timing) юм. 
Үүнийг ашиглан та өмнө тохируулах боломжтой хөдөлгөөнийг ашиглан нэг утгыг олон дахин анимейшн хийж боломжтой ба хүсвэл өөрөө ч хүссэнээрээ зохион хийх боломжтой. Анимейшнд ашиглагддаг хөдөлгөөний функц нь объектыг аажмаар хурдсах, удаашрах хөдөлгөөний зохицуулахад ерөнхийдөө тусалдаг.

`timing` нь цаанаасаа бүрэн хурдад хүрэх хүртлээ аажмаар нэмэгдэх муруйг ашигладаг ба аажмаар бууран зогсдог. Та налуу үүсэх өөр функцийг`easing` параметр ашиглан тодорхойлж өгөх боломжтой. Анимейшн эхлэхийн өмнө `duration` эсвэл `delay`-ыг өөрийнхөөрөө тохируулж мөн болно.
Жишээ нь бид нэг объектын 2 секундийн урттай, эцсийн байрлалдаа очихын өмнө бага зэрэг буцаж хөдөлдөг анимейшн хийе гэвэл:

```javascript
Animated.timing(this.state.xPosition, {
  toValue: 100,
  easing: Easing.back(),
  duration: 2000,
}).start();
```

`Animated` API хэсгийн [Configuring animations](animated.md#configuring-animations) гэснээс анимейшн хийхэд туслах тохиргооны параметрийн тухай уншиж судлаарай. 

### Анимейшн найруулан бичих

Анимейшн нь дэс дараатай эсвэл нэгэн зэрэг үйлдлийг хослуулсан байж болно. Дэс дараатай анимейшн нь өмнөх анимейшн дуусах үед шууд араас нь эхэлдэг эсвэл тодорхой хугацаанд түр зогссоны дараа эхэлдэг. `Animated` API нь `sequence()` болон `delay()` гэх мэт хэд хэдэн аргатай ба тэс бүр нь анимейшны массивыг авч ажиллуулан, хэрэгтэй үед `start()`/`stop()`-ыг дууддаг.

Жишээ нь, доорх анимейшн нь дорхноо зогсоод эн зэрэгцэн эргэх зуураа буцаж байна: 

```javascript
Animated.sequence([
  // decay, then spring to start and twirl
  Animated.decay(position, {
    // coast to a stop
    velocity: {x: gestureState.vx, y: gestureState.vy}, // velocity from gesture release
    deceleration: 0.997,
  }),
  Animated.parallel([
    // after decay, in parallel:
    Animated.spring(position, {
      toValue: {x: 0, y: 0}, // return to start
    }),
    Animated.timing(twirl, {
      // and twirl
      toValue: 360,
    }),
  ]),
]).start(); // start the sequence group
```

Хэрэв нэг анимейшн зогсох юм уу, гацвал тухайн группд байгаа бусад анимейшн ч мөн зогсоно. `Animated.parallel` нь `stopTogether` гэх сонголттой ба `false` гэдэг дээр тохируулж үүнийг идэвхгүй болгож болно.

Та `Animated` API-ын [Composing animations](animated.md#composing-animations)  хэсгээс найруулах арга техникийн тухай бүрэн жагсаалтыг хараарай.

### Хөдөлгөөнт утгыг нэгтгэх нь

Та [хөдөлгөөнт хоёр утгыг нэгтгэх](animated.md#combining-animated-values) боломжтой. Ингэхдээ нэмэх, үржүүлэх, хуваах үйлдэл эсвэл модуль ашиглан шинэ хөдөлгөөнт утга үүсгэдэг. 

Зарим тохиолдолд хөдөлгөөнт утга нь тооцогдохдоо өөр нэг хөдөлгөөнт утгад солигдох үе байна. Жишээ нь (2x --> 0.5x):

```javascript
const a = new Animated.Value(1);
const b = Animated.divide(1, a);

Animated.spring(a, {
  toValue: 2,
}).start();
```

### Интерполяц

Утга бүр интерполяцаар эхлээд дамжин өнгөрдөг. Интерполяц нь оролт, гаралтын цар хүрээг тодорхойлдог ба ингэхдээ шугаман интерполяц ашигладаг. Гэхдээ бас налуу функцыг дэмждэг. Анхны тохиргоогоор бол энэ нь муруйг тодорхойлсон цар хүрээг давж шилжүүлдэг. Гэхдээ тэ хүсвэл гаралтыг ямар нэг утга дээр барин тогтоож болно.

0-1 хүртэлх хүрээг 0-100 хүрээд хувиргах энгийн арга нь:

```javascript
value.interpolate({
  inputRange: [0, 1],
  outputRange: [0, 100],
});
```

Жишээ нь та `Animated.Value`-гаа 0-ээс 1 хүртэл явна гэж үзсэн ч байрлалыг нь 150 px-ээс 0px хүргэж хөдөлгөөнд оруулахыг хүссэн ч бүдгэрлийг нь 0-ээс 1 байхаар тохируулж болно. Үүнийг хийхдээ дээрх жишээ шиг хэрнээ `style` -ыг өөрчлөн хялбархан хийх боломжтой.

```javascript
  style={{
    opacity: this.state.fadeAnim, // Binds directly
    transform: [{
      translateY: this.state.fadeAnim.interpolate({
        inputRange: [0, 1],
        outputRange: [150, 0]  // 0 : 150, 0.5 : 75, 1 : 0
      }),
    }],
  }}
```

[`Интерполяц()`](animated.md#interpolate) нь олон төрлийн хүрээний сегментийг мөн дэмждэг ба хязгаарын бүсийг тодорхойлох болон хялбар арга ашиглахад тусалдаг. Жишээ нь -100 дээр 0 болдог, тэгээд 0 дээр 1 эргэж болоод буцаад 100 дээр тэг болон хязгаарын бүсэд хүрч цаашид 0 хэвээрээ байх харилцан хамаарлыг тогтоохын тулд:

```javascript
value.interpolate({
  inputRange: [-300, -100, 0, 100, 101],
  outputRange: [300, 0, 1, 0, 0],
});
```

Ингээд үүн шиг зураглал үүснэ:

```
Input | Output
------|-------
  -400|    450
  -300|    300
  -200|    150
  -100|      0
   -50|    0.5
     0|      1
    50|    0.5
   100|      0
   101|      0
   200|      0
```

`interpolate()` мөн spring зураглахыг дэмждэг. Ингэснээр та нэгж бүхий утгыг, мөн өнгийг анимейшнд ашиглаж болно. Жишээ нь та эргэлтийг хөдөлгөөнд оруулъя гэвэл:

```javascript
value.interpolate({
  inputRange: [0, 360],
  outputRange: ['0deg', '360deg'],
});
```

`интерполяц()` нь дурын муруйх функцтэй ба дийлэнх нь [`Easing`](easing.md) модульд аль хэдийн багтсан. 
`интерполяц()` нь мөн `outputRange` шилжихэд тохиргоо хийдэг. Та `extrapolate`, `extrapolateLeft`, эсвэл `extrapolateRight` гэснээс сонгож тохируулж болно. Анхны утга дээр `extend` гэж байгаа. Гэхдээ та гаралтын утга нь `outputRange`-ээс хэтрэхээс сэргийлэн `clamp` функцийг ашиглах боломжтой.

### Динамик утгыг дагах

Хөдөлгөөнт утга нь өөр утгыг дагаж болдог. Анимейшны өөр хөдөлгөөнт утгад  зүгээр тоо өгөхийн оронд `toValue`-ыг тохируулах нь зүйтэй. Жишээ нь Android-ын Messenger апп дээр ашиглагддаг "Chat Heads"  анимейшн нь өөр нэг хөдөлгөөнт утгын `spring()`-ээр эсвэл шууд дагах бол `timing()` болон `duration`-ыг ашиглан хийж болно. Мөн интерполяц ашиглан хийх боломжтой:

```javascript
Animated.spring(follower, {toValue: leader}).start();
Animated.timing(opacity, {
  toValue: pan.x.interpolate({
    inputRange: [0, 300],
    outputRange: [1, 0],
  }),
}).start();
```

 `Leader`, `follower` хөдөлгөөнт утгыг `Animated.ValueXY()` ашиглан хийнэ. `ValueXY` нь дүрсийг хөдөлгөх,чирэх гэх мэт 2D-тэй харилцан үйлчлэлийг хялбар болгодог. Хоёр янзын `Animated.Value` агуулдаг ба зарим туслах функцүүд тэднийг ашиглан дуудаж, ихэнх тохиолдолд `Value`-ын оронд `ValueXY`-ыг ашиглахад хүргэдэг. Ингэснээр дээрх жишээ дэх x болон y утгыг дагах боломжтой болно.

### Дохио дагах

Дүрс хөдөлгөх, гүйлгэх гэм мэт дохио болон бусад үйлдлийг [`Animated.event`] (animated.md#event) ашиглан шууд хөдөлгөөнт утгад шилжүүлэх боломжтой. Ингэхдээ нарийн бүтэцтэй синтакс зураглал ашигладаг ба утга нь үйл явдлын цогц объектоос гарна. Эхний шат нь массивыг олон параметр хөндлөн зураглах боломж олгодог ба энэхүү массив нь давхар объектууд агуулдаг. 

Жишээ нь хөндлөн гүйлгэх дохио хийх гэж байгаа бол та доорх маягаар `event.nativeEvent.contentOffset.x`-ыг `Animated.Value` болгоно: 

```javascript
 onScroll={Animated.event(
   // scrollX = e.nativeEvent.contentOffset.x
   [{ nativeEvent: {
        contentOffset: {
          x: scrollX
        }
      }
    }]
 )}
```

`PanResponder` ашиглаж байгаа үед та доорх кодыг ашиглан `gestureState.dx`, `gestureState.dy`-аас x болон y-ын байрлалыг гаргах боломжтой. Бид массивын эхний байрлалд `null` ашиглана. Яагаад гэвэл бид `gestureState` гэх  `PanResponder` -ын хоёр дахь параметрийг ашиглах сонирхолтой байгаа учраас. 

```javascript
onPanResponderMove={Animated.event(
  [null, // ignore the native event
  // extract dx and dy from gestureState
  // like 'pan.x = gestureState.dx, pan.y = gestureState.dy'
  {dx: pan.x, dy: pan.y}
])}
```

### Анимейшны одоогийн утгад хариу өгөх

Анимейшн хөдөлгөөн явагдаж байгаа үед утгыг унших боломж байхгүй гэдгийг та анзаарсан байх. Яагаад гэвэл оновчтой болгох үүднээс утга нь зөвхөн ажиллаж байгаа үед танигддаг. Хэрэв та одоогийн утгын хариу үйлдэл болгон JavaScript  ажиллуулах хэрэгтэй бол хоёр арга байна:

- `spring.stopAnimation(callback)` нь анимейшныг зогсоон эцсийн утгыг `callback` хийдэг. Дохионы шилжилт хийж байгаа үед энэ хэрэг болдог. 
- `spring.addListener(callback)` нь анимейшн ажиллаж байхад синхрон бусаар `callback` хийн, тухайн үеийн утгыг өгдөг. Төлөв өөрчлөх үед энэ нь хэрэг болдог. Тухайлбал хэрэглэгч шинэ сонголт дээр ойр чирэх үед томрох г.м. Энэ төрлийн төлөвийн томоохон өөрчлөлт нь 60 fps-ын дээр ажиллах үргэлжилсэн хөдөлгөөн болох гүйлгэх зэргийг бодвол бага зэрэг хожуу байхад үзүүлэх нөлөөлөл нь бага байдаг.

'Animated' нь бүрэн цуваалах боломжтой хийгдсэн бөгөөд ингэснээр энгийн Javascript event loop-аас тусдаа бие даан, сайн ажиллах боломжтой болох юм. Энэ нь API-д нөлөөлдөг ба бүрэн синхрон ажилладаг системтэй харьцуулахад ажиллахад бага зэрэг төвөгтэй гэдгийг анхаарна уу. Энэ мэт хязгаарлалттай хэрхэн ажиллах тухай `Animated.Value.addListener` гэснээс сонирхоно уу. Гэхдээ цаашид ажиллагаанд нөлөөлж магадгүй тул цөөн удаа ашиглахыг зөвлөе.

### Натив драйвер ашиглах 

`Animated` API нь цуваалах дизайнтай хийгдсэн. [Native driver](http://facebook.github.io/react-native/blog/2017/02/14/using-native-driver-for-animated.html) ашиглан бид анимейшнтэй холбоотой бүхнийг натив болгож, натив код frame бүрт холбогдохгүйгээр хэрэглэгчийн интерфэйс дээр анимейшн эхлүүлэх боломж олгодог. Анимейшн нь эхэлсэн л бол JS thread хаагдаж, анимейшнд нөлөөлөх боломжгүй болдог.

Энгийн анимейшнд натив драйвер ашиглах нь их хялбар. Ердөө эхлүүлэхдээ анимейшны тохиргоо дээр `useNativeDriver: true` гэснийг нэмэхэд л хангалттай.

```javascript
Animated.timing(this.state.animatedValue, {
  toValue: 1,
  duration: 500,
  useNativeDriver: true, // <-- Add this
}).start();
```

Хөдөлгөөнт утга нь зөвхөн нэг драйверт тохирсон байхаар хийгддэг. Хэрэв та анимейшнаа эхлүүлэхдээ натив драйвер ашиглах гэж байгаа бол тухайн утга дээр уг натив драйверыг бүх анимейшн ашиглаж байгаа эсэхийг нягтлаарай.

Натив драйвер нь `Animated.event`-тэй бас ажилладаг. React Native-ын зэрэгцээ бус ажиллах онцлогоос шалтгаалан натив драйвергүйгээр анимейшн нь цаанаа үргэлж frame ажиллуулж байдаг тул scroll хийх байрлал бүхий анимейшн хийхэд тохиромжтой.

```javascript
<Animated.ScrollView // <-- Use the Animated ScrollView wrapper
  scrollEventThrottle={1} // <-- Use 1 here to make sure no events are ever missed
  onScroll={Animated.event(
    [
      {
        nativeEvent: {
          contentOffset: {y: this.state.animatedValue},
        },
      },
    ],
    {useNativeDriver: true}, // <-- Add this
  )}>
  {content}
</Animated.ScrollView>
```

Та [RNTester app](https://github.com/facebook/react-native/blob/master/RNTester/) ажиллуулан, натив хөдөлгөөнт жишээ ачаалан натив драйвер хэрхэн ажилладгийг харж болно.  Мөн жишээ болгон хийсэн зүйлс нь хэрхэн бүтдэг тухай [source code](https://github.com/facebook/react-native/blob/master/RNTester/js/NativeAnimationsExample.js) гэснээс хараарай.

#### Санамж

`Animated` дээр хийсэн бүхнийг натив драйвер дэмжинэ гэж ойлгож болохгүй. Та зөвхөн non-layout properties буюу `transform`, `opacity`  зэргийг хөдөлгөөнт болгох боломжтой. Flexbox болон байрлал дээр бол ашиглаж болохгүй. `Animated.event` ашиглаж байгаа үед зөвхөн шууд хийх боломжтой үйлдэлд ашиглагдана. Энэ нь `PanResponder`-тай бол ажиллахгүй, харин `ScrollView#onScroll` гэх мэттэй ажиллана гэсэн үг юм.

Анимейшн явж байх үед `VirtualizedList` компонентыг нэмж эгнээ рендэр хийхээс сэргийлдэг. Хэрэв та хэрэглэгч жагсаалт гүйлгэж байх үед урт, давталттай анимейшн ажиллуулахыг хүсвэл анимейшны тохиргоо хийхдээ `isInteraction: false` ашиглаж, үүнээс зайлсхийх боломжтой.

### Анхаарах

`rotateY`, `rotateX` болон бусад шилжилтийн хэв маягийг ашиглаж байгаа үед `perspective` байрандаа байгаа эсэхийг шалгаарай. Одоогоор Android дээр энэ байхгүй бол зарим анимейшн рендэр хийхгүй байгаад байгаа. Жишээг доор харууллаа.

```javascript
<Animated.View
  style={{
    transform: [
      {scale: this.state.scale},
      {rotateY: this.state.rotateY},
      {perspective: 1000}, // without this line this Animation will not render on Android while working fine on iOS
    ],
  }}
/>
```

### Нэмэлт жишээнүүд

RNTester аппаас `Animated` ашигласан олон янзын жишээ харж болно:

- [AnimatedGratuitousApp](https://github.com/facebook/react-native/tree/master/RNTester/js/AnimatedGratuitousApp)
- [NativeAnimationsExample](https://github.com/facebook/react-native/blob/master/RNTester/js/NativeAnimationsExample.js)

## `LayoutAnimation` API

`LayoutAnimation`-ыг ашиглан дараагийн рендэр,  layout мөчлөгт бүгдэд нь харагдах анимейшнаа  `create` , `update` хийх боломжтой. Шууд хөдөлгөөнд оруулахын тулд нарийн хэмжиж, тооцоолохгүйгээр flexbod layout-шинэчлэхэд хэрэг болох ба layout-д хийсэн өөрчлөлт нь удамшил авсан зүйлдээ нөлөөлөх магадлалтай. Жишээ нь, "see more"  өргөтгөл нь эцгийнхээ хэмжээг нэмэн, доод мөрийг шахдаг. Тэгэхгүй бол бүгдийг нэг зэрэг хөдөлгөөнт оруулахад компонентуудад тодорхой зохицуулалт шаардлагатай болно.

`LayoutAnimation` нь их чадалтай, хэрэгтэй ч гэсэн `Animated` болон бусад анимейншны сантай харьцуулахад удирдах чадал нь тааруу гэдгийг анхаарна уу. Тиймээс `LayoutAnimation` ашиглан хүссэн зүйлээ хийхийн тулд  өөр арга хайх хэрэгтэй. 

**Android**  дээр үүнийг ажиллуулахын тулд та `UIManager` ашиглан доорх тохиргоог хийх шаардлагатай:

```javascript
UIManager.setLayoutAnimationEnabledExperimental &&
  UIManager.setLayoutAnimationEnabledExperimental(true);
```

```SnackPlayer
import React from 'react';
import {
  NativeModules,
  LayoutAnimation,
  Text,
  TouchableOpacity,
  StyleSheet,
  View,
} from 'react-native';

const { UIManager } = NativeModules;

UIManager.setLayoutAnimationEnabledExperimental &&
  UIManager.setLayoutAnimationEnabledExperimental(true);

export default class App extends React.Component {
  state = {
    w: 100,
    h: 100,
  };

  _onPress = () => {
    // Animate the update
    LayoutAnimation.spring();
    this.setState({w: this.state.w + 15, h: this.state.h + 15})
  }

  render() {
    return (
      <View style={styles.container}>
        <View style={[styles.box, {width: this.state.w, height: this.state.h}]} />
        <TouchableOpacity onPress={this._onPress}>
          <View style={styles.button}>
            <Text style={styles.buttonText}>Press me!</Text>
          </View>
        </TouchableOpacity>
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    alignItems: 'center',
    justifyContent: 'center',
  },
  box: {
    width: 200,
    height: 200,
    backgroundColor: 'red',
  },
  button: {
    backgroundColor: 'black',
    paddingHorizontal: 20,
    paddingVertical: 15,
    marginTop: 15,
  },
  buttonText: {
    color: '#fff',
    fontWeight: 'bold',
  },
});
```
Энэ жишээнд утга нь өмнө нь өгөгдсөн байгаа. Та анимейшнаа хүссэнээрээ өөрчлөлт болно. [LayoutAnimation.js](https://github.com/facebook/react-native/blob/master/Libraries/LayoutAnimation/LayoutAnimation.js)-аас дэлгэрэнгүй мэдээллийг харна уу.

## Нэмэлт тэмдэглэл

### `requestAnimationFrame`

`requestAnimationFrame` нь хөтөч дээр байдаг polyfill гэдгийг та мэдэх байх. Энэ нь ямарваа үйлдлийг цор ганц параметр гэж үзэн дараагийн дахин зурах явцаас өмнө дууддаг. Анимейшн хийхэд тун чухал зүйл бөгөөд Javascript дээр суурилсан анимейшны бүх API-уудын үндэс нь болдог. Ерөнхийдөө та өөрөө дуудах хэрэггүй. Анимейшны API-ууд нь frame шинэчлэлийг хийчихнэ. 

### `setNativeProps`

[Direct Manipulation](direct-manipulation.md) хэсэгт дурдсанчлан`setNativeProps` нь натив суурьтай компонентуудын (холимог компонентуудыг бодвол жинхэнээсээ натив үзэлтээр баталгаажсан) тохиргоог `setState`-гүйгээр, компонентын шатлалыг дахин рендэр хийхгүйгээр шууд хийхэд ашиглагддаг. 

Бид үүнийг Rebound-ын жишээ дээр ашиглаж, scale-ыг шинэчлэх боломжтой. Бидний шинэчилж байгаа компонент нь өөр нэг компонентын дотор агуулагдсан,  `shouldComponentUpdate` ашиглан тодорхойлогдоогүй бол энэ арга нь тун хэрэгтэй байх болно.

Хэрэв таны анимейшны frame нь унаад (секундэд 60-аас доош frame ажиллуулах) байх юм бол `setNativeProps` эсвэл `shouldComponentUpdate` ашиглан оновчтой тохируулж өгөх хэрэгтэй. Эсвэл та [NativeDriver](http://facebook.github.io/react-native/blog/2017/02/14/using-native-driver-for-animated.html) ашиглан JavaScript thread дээр биш UI thread дээр анимейшнаа ажиллуулж болно. Анимейшн гүйцэт болох хүртэл та [InteractionManager](interactionmanager.md) ашиглан тооцоолох ажлыг хойшлуулж болно. Апп дээр хөгжүүлэгчийн цэсийн "FPS Monitor" -ыг ашиглан frame rate-ыг хянах боломжтой.
