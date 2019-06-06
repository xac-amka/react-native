---
id: platform-specific-code
title: Тухайн платформд зориулсан код
---

Платформ дамжин ажиллаж чадах апп хийх үед та бичсэн кодоо аль болох дахин ашиглахыг хүсэх нь лавтай. Гэхдээ кодыг заавал өөрөөр хийх шаардлагатай нөхцөл байдал мөн үүсэх магадлалтай . Тухайлбал та харагдах байдлын компонентыг iOS болон Android-д тус тусад нь хийхийг хүсэж болно.

React Native нь кодоо хялбар зохицуулж, платформд зориулан тусгаарлах хоёр арга санал болгодог.

- [`Platform` модуль](platform-specific-code.md#platform-module) ашиглах.
- [platform-specific file extensions](platform-specific-code.md#platform-specific-extensions) ашиглах.

Зарим нэг компонентууд нь зөвхөн тухайн нэг платформ дээр ажиллах хэсэгтэй байж болно. Эдгээр бүх проп нь `@platform` гэсэн тэмдэглэгээтэй байх ба вэбсайт дээр хажуудаа жижиг ялгах тэмдэгтэй байдаг.

## Платформ модуль

React Native-т тухайн апп ажиллаж байгаа платформыг таних модуль байдаг. Энэхүү таних функцийг ашиглан тухайн платформд зориулсан код ажиллуулах боломжтой. Компонентийн багахан хэсэг нь ямар нэг платформд зориулсан байх шаардлагатай бол энэ аргыг ашиглаарай.

```javascript
import {Platform, StyleSheet} from 'react-native';

const styles = StyleSheet.create({
  height: Platform.OS === 'ios' ? 200 : 100,
});
```

`Platform.OS` will be `ios` when running on iOS and `android` when running on Android.

Мөн `Platform.select` арга бий. Platform.OS-ыг түлхүүр хэлбэрээр агуулсан объект байгаа үед одоо ашиглаж байгаа платформ дээрээс утгыг авдаг.

```javascript
import {Platform, StyleSheet} from 'react-native';

const styles = StyleSheet.create({
  container: {
    flex: 1,
    ...Platform.select({
      ios: {
        backgroundColor: 'red',
      },
      android: {
        backgroundColor: 'blue',
      },
    }),
  },
});
```

Үүний дүнд хоёр платформ дээр `flex: 1`-тэй контейнер дотор үүснэ. iOS дээр улаан суурь өнгөтэй, Android дээр цэнхэр суурь өнгөтэй байна.

`ямар ч` утга оруулж болох тул та доорх шиг тодорхой платформд зориулсан компонент буцаахад ашиглаж болно:

```javascript
const Component = Platform.select({
  ios: () => require('ComponentIOS'),
  android: () => require('ComponentAndroid'),
})();

<Component />;
```

### Android хувилбарыг таних

Android дээр `Platform` модулийг апп ажиллаж байгаа Android платформын нь хувилбарыг танихад ашиглаж болно:

```javascript
import {Platform} from 'react-native';

if (Platform.Version === 25) {
  console.log('Running on Nougat!');
}
```

### iOS хувилбарыг таних

iOS дээр `Version` гэдэг `-[UIDevice systemVersion]`-ын үр дүн юм. Энэ нь одоогийн үйлдлийн системийн string юм. Энэхүү системийн хувилбарын нэг жишээ бол "10.3". Жишээ нь iOS дээр их хувилбарын дугаарыг танихад:

```javascript
import {Platform} from 'react-native';

const majorVersionIOS = parseInt(Platform.Version, 10);
if (majorVersionIOS <= 9) {
  console.log('Work around a change in behavior');
}
```

## Тухайн платформд зориулсан өргөтгөл

Тухайн платформд зориулсан код нь их нарийн бол та кодоо тусдаа файлууд болгож хуваах нь зүйтэй. React Native нь файлыг `.ios.` эсвэл `.android.` гэж таньдаг бөгөөд бусад компонентуудаас шаардлагатай үед холбогдох платформыг ажиллуулдаг.

Жишээ нь, танд доорх файлууд байлаа гэж бодъё:

```sh
BigButton.ios.js
BigButton.android.js
```

Та доорх маягаар компонентоо дуудаж болно:

```javascript
import BigButton from './BigButton';
```

React Native ачаалж байгаа платформ дээр үндэслэн зөв файлыг сонгодог.

## Тухайн нативт зориулсан өргөтгөл ( NodeJS болон Web-д код хуваалцах)

Модуль NodeJS/Web болон React Native-ын хооронд хорших хэрэгтэй агаад Android/iOS-т ялгаагүй байх бол та `.native.js` гэсэн өргөтгөлийг ашиглах боломжтой. React Native болон ReactJS-ын дунд хуваалцах түгээмэл кодтой юм дээр ажиллаж байгаа бол энэ танд илүү хэрэг болно.

Жишээ нь, танд доорх файлууд байлаа гэж бодъё:

```sh
Container.js # picked up by Webpack, Rollup or any other Web bundler
Container.native.js # picked up by the React Native bundler for both Android and iOS (Metro)
```

Та `.native` өргөтгөлгүйгээр доорх байдлаар дуудаж болно:

```javascript
import Container from './Container';
```

**Мэргэжлийн зөвлөгөө:** Хэрэглэхгүй кодтой байхаас сэргийлж, bundle-ийн сүүлийн хэмжээг багасгахын тулд вэб багцлагч (bundler)-аа тохируулахдаа `.native.js` өргөтгөлийг хэрэгсэхгүй орхих хэрэгтэй.
