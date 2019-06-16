---
id: keyboard
title: Keyboard
---

`Keyboard` модуль нь нь удирдах товчлуурт ирсэн үйлдлийг зохицуулдаг. 

### Хэрэглээ

Удирдах товчлуурын модулийн тусламжтай та натив эвентүүдийг хүлээн авч, хариу үйлдэл хийхийн сацуу товчлуурт ирсэн дохиог үл харгалзан орхих гэх мэтээр өөрчлөлтийг хийх боломжтой. 

```javascript
import React, {Component} from 'react';
import {Keyboard, TextInput} from 'react-native';

class Example extends Component {
  componentDidMount() {
    this.keyboardDidShowListener = Keyboard.addListener(
      'keyboardDidShow',
      this._keyboardDidShow,
    );
    this.keyboardDidHideListener = Keyboard.addListener(
      'keyboardDidHide',
      this._keyboardDidHide,
    );
  }

  componentWillUnmount() {
    this.keyboardDidShowListener.remove();
    this.keyboardDidHideListener.remove();
  }

  _keyboardDidShow() {
    alert('Keyboard Shown');
  }

  _keyboardDidHide() {
    alert('Keyboard Hidden');
  }

  render() {
    return <TextInput onSubmitEditing={Keyboard.dismiss} />;
  }
}
```

### Аргачлал

- [`addListener`](keyboard.md#addlistener)
- [`removeListener`](keyboard.md#removelistener)
- [`removeAllListeners`](keyboard.md#removealllisteners)
- [`dismiss`](keyboard.md#dismiss)

---

# Тайлбар

## Аргууд

### `addListener()`

```javascript
static addListener(eventName, callback)
```

`addListener` функц нь JavaScript функцийг удирдах товчлуурт ирсэн танигдсан натив үйлдэлтэй холбож өгдөг. 

Энэхүү функц нь тухайн тайлбарыг үйлдэл хийсэн сонсогчид эргээд хүргэдэг. 


@param {string} eventName `nativeEvent` гэдэг нь хүлээн авч буй үйлдлийг таньдаг стринг юм. Доорхын аль нэг нь байх боломжтой:

- `keyboardWillShow`
- `keyboardDidShow`
- `keyboardWillHide`
- `keyboardDidHide`
- `keyboardWillChangeFrame`
- `keyboardDidChangeFrame`

Хэрэв та `android:windowSoftInputMode`-ыг `adjustResize` эсвэл `adjustNothing` гэдэг дээр тохируулбал зөвхөн `keyboardDidShow` болон `keyboardDidHide` гэсэн эвентүүд Android дээр харагдах болно. Хариу үйлдэлх хийх натив эвент байхгүй тул `keyboardWillShow` , `keyboardWillHide` нар нь ерөнхийдөө Android дээр байдаггүй.


@param {function} гэдэг нь эвент эхлэх үед дуудагддаг эргэн дуудах функц юм. 

---

### `removeListener()`

```javascript
static removeListener(eventName, callback)
```

Тодорхой нэг сонсогчийг арилгах.


@param {string} eventName The `nativeEvent` нь таны сонсож байгаа эвентийг танихад тусалдаг стринг юм. 
@param {function} нь эвент эхлэх үед дуудагддаг эргэн дуудах функц юм. 

---

### `removeAllListeners()`

```javascript
static removeAllListeners(eventName)
```
Тодорхой нэг төрлийн эвентийн бүх сонсогчийг арилгах.

@param {string} eventType натив эвентийн харж буй сонсогчыг устгах болно. 

---

### `dismiss()`

```javascript
static dismiss()
```

Удирдах товчлуурын идэвхтэй үйлдлийг үл харгалзан, төвлөрөхгүй байлгана.

