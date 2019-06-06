---
id: backhandler
title: BackHandler
---

Буцах үйлдлийг хийхийн тулд төхөөрөмжийн товчлуурыг дарах event-ийг илрүүлэх

Android: Төхөөрөмжөөс буцах товчлуур дарагдах үеийн event-ийг илрүүлэх. Энэ эвентийг сонсож байгаа сонсогч байхгүй эсвэл true утгийг буцаасан ямар ч сонсогч байхгүй үед буцах товч дарагдахад угийн хийгддэг үйлдэл болох "аппаас гарах" үйлдлийг хийнэ.

tvOS: Телевизийн удирдлагын "цэс" товчлуурыг дарах event-ийг илрүүлэх. (Одоо хүртэл хийгдэж байгаа: Энэ эвентийг сонсож байгаа сонсогч байхгүй эсвэл true утгийг буцаасан ямар ч сонсогч байхгүй үед буцах товч дарагдахад хийгдэх "аппаас гарах" үйлдлийг болиулна.)

ios: IOS дээр ажиллахгүй.

Энэ event-ийн сонсогч нар нь сүүлд бүртгэгдсэнээсээ эхлэн дуудагддаг ба хэрвээ аль нэг нь true утга буцаавал өмнө нь бүртгэгдсэн сонсогчууд нь дуудагдахгүй.

Жишээ нь:

```javascript
BackHandler.addEventListener('hardwareBackPress', function() {
  // this.onMainScreen болон this.goBack нь зүгээр жишээ юм. Энд өөрийнхөө кодыг бичих хэрэгтэй
  // Өмнөх төлөв рүү үсрэх үйлдлийг хийж болох юм.
  
  // this.onMainScreen and this.goBack are just examples, you need to use your own implementation here
  // Typically you would use the navigator here to go to the last state.

  if (!this.onMainScreen()) {
    this.goBack();
    return true;
  }
  return false;
});
```
React Native-ын амьдралын мөчлөгтэй холбосон жишээ:

```javascript
  componentDidMount() {
    this.backHandler = BackHandler.addEventListener('hardwareBackPress', this.handleBackPress);
  }

  componentWillUnmount() {
    this.backHandler.remove()
  }

  handleBackPress = () => {
    this.goBack(); // энэ goBack функц нь async функц бол илүү төгс ажиллана works best when the goBack is async
    return true;
  }
```
React Native-ын амьдралын мөчлөгтэй холбосон бас нэг жишээ:
Lifecycle alternative:

```javascript
  componentDidMount() {
    this.backHandler = BackHandler.addEventListener('hardwareBackPress', () => {
      this.goBack(); // энэ goBack функц нь async функц бол илүү төгс ажиллана
      return true;
    });
  }

  componentWillUnmount() {
    this.backHandler.remove();
  }
```

### Methods

- [`exitApp`](backhandler.md#exitapp)
- [`addEventListener`](backhandler.md#addeventlistener)
- [`removeEventListener`](backhandler.md#removeeventlistener)

---

# Reference

## Methods

### `exitApp()`

```javascript
static exitApp()
```

---

### `addEventListener()`

```javascript
static addEventListener(eventName, handler)
```

---

### `removeEventListener()`

```javascript
static removeEventListener(eventName, handler)
```
