---
id: timers
title: Цаг тоолуур
---

Цаг тоолуур нь аппликейшны чухал нэг хэсэг бөгөөд React Native нь [browser timers](https://developer.mozilla.org/en-US/Add-ons/Code_snippets/Timers) ашигладаг.

## Цаг тоолуур

- setTimeout, clearTimeout
- setInterval, clearInterval
- setImmediate, clearImmediate
- requestAnimationFrame, cancelAnimationFrame

`requestAnimationFrame(fn)` нь `setTimeout(fn, 0)`-тай адилгүй. Эхнийх нь бүх frame гүйцсэний дараа ажиллаж эхэлнэ. Харин сүүлийнх нь тэр дороо ажиллана (iPhone 5S дээр секундэд 1000 удаа).

`setImmediate` гэдэг нь натив руу нэгтгэсэн хариу илгээхээс өмнө одоогийн Javascript блокийн төгсгөлд хийгдэнэ.  Хэрэв та `setImmediate` доторх `setImmediate`-ыг дуудвал тэр дороо ажиллах ба натив хооронд ажиллахгүй. 

`Promise` нь `setImmediate` асинхрон команд болгон ашигладаг.

## InteractionManager

Сайн хийгдсэн натив аппын ажиллагаа нь сайн байдаг нэг учир нь харилцан үйлдэл хийх, анимейшн зэргээс зайлсхийдэгт оршдог.   React Native-т ганцхан JS ажиллуулах thread-ээр хязгаарлагдаж байгаа. Гэхдээ та `InteractionManager` ашиглаж аливаа харилцан үйлдэл, анимейшны дууссаны дараа ажиллах урт хугацаанд үйлдлийг хийхээр тохируулж болно.

Харилцан үйлдэл дууссаны дараа аливаа ажлыг гүйцэтгэх хугацааг доорх маягаар зааж өгнө:

```javascript
InteractionManager.runAfterInteractions(() => {
  // ...long-running synchronous task...
});
```
Үүнийг бусад цаг тохируулах сонголтуудтай харьцуулж үзээрэй:

- requestAnimationFrame(): аливаа харагдацыг хөдөлгөөнд оруулах кодод зориулсан.
- setImmediate/setTimeout/setInterval(): кодыг дараа нь ажиллуулна. Энэ нь анимейшныг удаашруулах магадлалтай гэдгийг анхаарна уу. 
- runAfterInteractions(): кодыг дараа ажиллуулна. Анимейшныг удаашруулахгүйгээр.

Дэлгэцэд хүрэхийг таньдаг систем нь нэг эсвэл түүнээс дээш удаа хүрэхийг 'interaction' буюу харилцан үйлдэл гэж үзэх бөгөөд бүрэн дарж дуусах эсвэл үйлдэл цуцлах хүртэл `runAfterInteractions()`-ыг хойшлуулдаг. 

InteractionManager нь анимейшны эхлэлд 'handle' гэх харилцан үйлдлийг үүсгэн анимейшнуудыг бүртгэж, гүйцсэний дараа арилгадаг:

```javascript
var handle = InteractionManager.createInteractionHandle();
// run animation... (`runAfterInteractions` tasks are queued)
// later, on animation completion:
InteractionManager.clearInteractionHandle(handle);
// queued tasks run if all handles were cleared
```

## TimerMixin

React Native дээр хийгдсэн аппуудад гардаг том алдаанууд нь компонент салгагдсан байх үед цаг тоолуур ажиллаж эхэлснээс болдог болохыг бид олж мэдсэн юм.  Энэ асуудлыг шийдэхийн тулд бид `TimerMixin`-ыг гаргасан. Хэрэв та `TimerMixin` ашиглавал `setTimeout(fn, 500)`-д дуудсан зүйлсээ `this.setTimeout(fn, 500)` болгон солиход ( `this` нэмэхэд л болно) компонент салгагдах үед бүгд цэвэр байх болно. 

Энэхүү сан нь React Native-т ажиллахгүй. Төсөлдөө ашиглахын тулд та `npm i react-timer-mixin --save` суулгах шаардлагатай.


```javascript
import TimerMixin from 'react-timer-mixin';

var Component = createReactClass({
  mixins: [TimerMixin],
  componentDidMount: function() {
    this.setTimeout(() => {
      console.log('I do not leak!');
    }, 500);
  },
});
```
Компонент салгагдсан үед ажиллах гэх зэргээс болж ажиллахгүй байх гэхчлэн алдааг хайх ажлаас энэ нь таныг чөлөөлөх юм. 

Хэрэв та React компонентууддаа ES6 классууд ашиглах бол [mixin-д зориулсан цаанаас API байдаггүй гэдгийг анхаарна уу](https://facebook.github.io/react/blog/2015/01/27/react-v0.13.0-beta-1.html#mixins). ES6 классуудад `TimerMixin` ашиглах бол 
[react-mixin](https://github.com/brigand/react-mixin) гэдгийг сонирхоно уу.
