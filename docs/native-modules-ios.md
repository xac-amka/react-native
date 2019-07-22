---
id: native-modules-ios
title: Натив модулиуд
---

Заримдаа апп нь React Native-ын зохих хариу өгөх модульгүйгээр платформ API-д хандах хэрэгтэй болдог. Магадгүй Javascript-руу дахин өөрчлөхгүйгээр бэлэн байгаа Objective-C, Swift эсвэл C++ код ашиглах эсвэл зураг процесс хийх, өгөгдлийн сан эсвэл ахисан түвшний өргөтгөл гэх мэтэд зориулсан ажиллагааг сайжруулах, олон процесст зориулсан код бичих хэрэг гарч болно.

Бид React Native-ыг хүн өөрөө натив код бичих боломжтой байхаар загварчилсан ба платформыг бүрэн ашиглах боломжийг та бүхэнд олгохыг хүссэн. Энэ нь илүү ахисан түвшний функц бөгөөд бид энгийн хөгжүүлэлтийн явцад төдийлөн ашиглагдахгүй байх гэж бодож байна. Гэхдээ байх нь чухал. Хэрэв React Native-т танд хэрэгтэй натив функц байхгүй бол та өөрөө хийх боломжтой юм. 

Натив модуль хэрхэн үүсгэх тухай ахисан түвшний заавар бий.  Objective-C эсвэл Swift болон гол сангуудын талаар (Foundation, UIKit) мэдлэгтэй хүмүүст зориулсан заавар байгаа. 


## Натив модулийн тохиргоо

Натив модулиуд нь ихэвчлэн npm пакэж хэлбэрээр байдаг. Энгийн javascript файлууд, зүйлсээс бусдаар бол тэд нь Android сангийн төслүүд агуулсан байна. Энэхүү төсөл нь NPM-ын талаас бол бусад медиа төрлийн зүйл байх юм. Энэ нь ямар нэг онцгой зүйлгүй гэсэн үг. Код автоматаар үүсгэх тухай үндсэн ойлголттой болохыг хүсвэл [Натив Модулийн Тохиргоо](native-modules-setup) гэснийг уншина уу.

## iOS Календар Модулийн жишээ 

Энэхүү зааварт [iOS Calendar API](https://developer.apple.com/library/mac/documentation/DataManagement/Conceptual/EventKitProgGuide/Introduction/Introduction.html)-ыг жишээ болгон ашигласан. Javascript-ээр iOS хуанли гаргадаг болгох гээд үзье.

Натив модуль гэдэг нь `RCTBridgeModule` протокол бүхий нэг Objective-C класс юм. RCT нь ReaCT-ын товчлол юм шүү.  

```objectivec
// CalendarManager.h
#import <React/RCTBridgeModule.h>

@interface CalendarManager : NSObject <RCTBridgeModule>
@end
```
`RCTBridgeModule`  протоколоос гадна классдаа `RCT_EXPORT_MODULE() макрог оруулах ёстой. Javascript кодоор хандах боломжтой модулийн нэрийг тодорхойлох сонголт бүхий аргументыг гаргадаг (Энэ талаар дараа дэлгэрэнгүй тайлбарлах болно). Хэрэв та нэр тодорхойлж өгөхгүй бол Javascript модулийн нэр нь Objective-C классын нэртэй адилхан байна. Хэрэв Objective-C классын нэр нь RCT гэж эхэлж байвал JavaScript модуль нь RCT гэсэн угтваргүй байна.


```objectivec
// CalendarManager.m
#import "CalendarManager.h"

@implementation CalendarManager

// To export a module named CalendarManager
RCT_EXPORT_MODULE();

// This would name the module AwesomeCalendarManager instead
// RCT_EXPORT_MODULE(AwesomeCalendarManager);

@end
```

Зориуд заагаагүй л бол React Native нь `CalendarManager`-ын ямар ч методыг Javascript руу хуулахгүй. Үүний тулд `RCT_EXPORT_METHOD()` макро ашиглана:

```objectivec
#import "CalendarManager.h"
#import <React/RCTLog.h>

@implementation CalendarManager

RCT_EXPORT_MODULE();

RCT_EXPORT_METHOD(addEvent:(NSString *)name location:(NSString *)location)
{
  RCTLogInfo(@"Pretending to create an event %@ at %@", name, location);
}

@end
```

Одоо Javascript файлаасаа та методоо дуудаж болно:

```javascript
import {NativeModules} from 'react-native';
var CalendarManager = NativeModules.CalendarManager;
CalendarManager.addEvent('Birthday Party', '4 Privet Drive, Surrey');
```

> **ТЭМДЭГЛЭЛ**: JavaScript метод нэрс

> Javascript руу оруулсан методын нр нь анхны колоны натив методын нэр байна. React Native-т`RCT_REMAP_METHOD()` гэх макро байх ба энэ н Javascript методын нэрийг тодорхойлж өгөх зорилготой юм. Эхний колонд олон тооны натив метод байгаа үед энэ нь тустай бөгөөд Javascript-ын нэрүүд нь холилдохоос сэргийлнэ.  


CalendarManager модуль нь  [CalendarManager new] ашиглан Objective-C  дээр үүсдэг. Bridge method-ын буцах утга нь үргэлж `void` байна. React Native bridge нь асинхрон учраас Javascript руу үр дүнг дамжуулах ганц арга нь буцааж дуудах эсвэл эвент өгөх юм (доорхыг харна уу).
is asynchronous, so the only way to pass a result to JavaScript is by using callbacks or emitting events (see below).

## Аргументын төрлүүд

`RCT_EXPORT_METHOD` нь бүх стандарт JSON объектын төрлийг дэмждэг.Үүнд:

- string (`NSString`)
- number (`NSInteger`, `float`, `double`, `CGFloat`, `NSNumber`)
- boolean (`BOOL`, `NSNumber`)
- array (`NSArray`) of any types from this list
- object (`NSDictionary`) with string keys and values of any type from this list
- function (`RCTResponseSenderBlock`)

Гэхдээ бас `RCTConvert` класс дэмждэг ямар ч төрөлтэй ажилладаг([Дэлгэрэнгүйг `RCTConvert`-ээс уншина уу](https://github.com/facebook/react-native/blob/master/React/Base/RCTConvert.h)).  `RCTConvert` туслах бүх функц нь JSON утгыг хүлээн авч, натив Objective-C  төрөл эсвэл класс гэж мап хийдэг. 

Бидний `CalendarManager` жишээ дээр бид эвентийн огноог натив метод руу дамжуулах хэрэгтэй байгаа. JavaScript огноо заасан объектыг bridge-ээр илгээж чадахгүй учраас бид огноог стринг эсвэл тоонд шилжүүлэх хэрэгтэй. Натив функцийг ингэж бичих боломжтой:

```objectivec
RCT_EXPORT_METHOD(addEvent:(NSString *)name location:(NSString *)location date:(nonnull NSNumber *)secondsSinceUnixEpoch)
{
  NSDate *date = [RCTConvert NSDate:secondsSinceUnixEpoch];
}
```

эсвэл үүн шиг:

```objectivec
RCT_EXPORT_METHOD(addEvent:(NSString *)name location:(NSString *)location date:(NSString *)ISO8601DateString)
{
  NSDate *date = [RCTConvert NSDate:ISO8601DateString];
}
```
Төрлийг автоматаар өөрчилдөг функцийг ашиглах боломжтой бөгөөд доорхыг бичихэд л хангалттай:

```objectivec
RCT_EXPORT_METHOD(addEvent:(NSString *)name location:(NSString *)location date:(NSDate *)date)
{
  // Date is ready to use!
}
```

Тэгээд  JavaScript-ээс үүнийг дуудахдаа ингэнэ:

```javascript
CalendarManager.addEvent(
  'Birthday Party',
  '4 Privet Drive, Surrey',
  date.getTime(),
); // passing date as number of milliseconds since Unix epoch
```

эсвэл

```javascript
CalendarManager.addEvent(
  'Birthday Party',
  '4 Privet Drive, Surrey',
  date.toISOString(),
); // passing date as ISO-8601 string
```

Утгууд нь хоёулаа `NSDate` нативт зөв шилжинэ. `Array` гэхчлэн буруу утга байвал "Redbox" алдааны мессеж гарч ирнэ.

`CalendarManager.addEvent` метод нь илүү арвин болох тусам аргументын тоо өснө. Зарим нэгийг нь сонгож оруулдаг байж болно. Энэ тохиолдолд API-г бага зэрэг өөрчилж, эвент аттрибутын dictionary-ыг хүлээн авах хэрэгтэй болно:


```objectivec
#import <React/RCTConvert.h>

RCT_EXPORT_METHOD(addEvent:(NSString *)name details:(NSDictionary *)details)
{
  NSString *location = [RCTConvert NSString:details[@"location"]];
  NSDate *time = [RCTConvert NSDate:details[@"time"]];
  ...
}
```

тэгээд JavaScript-ээс дуудна:

```javascript
CalendarManager.addEvent('Birthday Party', {
  location: '4 Privet Drive, Surrey',
  time: date.getTime(),
  description: '...',
});
```

> **Тэмдэглэл**: Массив болон мапийн тухай
>
> Objective-C нь эдгээр бүтцэд ямар төрлийн утга байх вэ гэдэгт баталгаа өгдөггүй. Натив модуль чинь стринг бүхий массив хүлээн авахаар байж болно. Хэрэв Javascript таны методыг дуудахдаа тоо, стринг агуулсан массив гээд дуудвал та `NSNumber` болон `NSString` агуулсан `NSArray` авна. Массивын тухайд `RCTConvert`  нь `NSStringArray`,  `UIColorArray` гэх мэт методоо зарлах үед ашиглаж болох зарим төрлийн коллекцыг өгдөг. Мапийн тухайд гэвэл `RCTConvert` туслах методыг зориуд өөрөө дуудан нэг бүрчлэн утгыг шалгах нь хөгжүүлэгчийн хийх ажил байдаг. 

## Callbacks

> **АНХААРУУЛГА**
>
> Callbacks-тай холбоотой яг баттай туршлага хомс учраас энэ хэсэгтэй байгаа мэдээлэл нь илүүтэй туршилтын чанартай гэж ойлгож болно. 

Натив модулиуд нь мөн callback гэх онцгой төрлийн аргументыг дэмждэг. Ихэнх тохиолдолд үр дүнг Javascript руу дуудахад ашигладаг.

```objectivec
RCT_EXPORT_METHOD(findEvents:(RCTResponseSenderBlock)callback)
{
  NSArray *events = ...
  callback(@[[NSNull null], events]);
}
```

`RCTResponseSenderBlock` нь ганцхан аргумент хүлээн зөвшөөрдөг.  Энэ нь JavaScript callback-т дамжуулах параметруудын массив юм. Энэ тохиолдолд бид  Node-ын тогтсон ажиллагааг ашиглан эхний параметрийг алдаатай объект болгоно (ихэнхдээ алдаагүй үед `null`  байна). Бусад нь уг функцынхээ үр дүн байх юм. 

```javascript
CalendarManager.findEvents((error, events) => {
  if (error) {
    console.error(error);
  } else {
    this.setState({events: events});
  }
});
```
Аливаа натив модуь нь callback-аа яг нэг удаа дуудана. Callback-ыг хадгалаад дараа нь дуудаж болдог. Энэхүү үйлдлийг делегат шаарддаг iOS API-уудыг врап хийхэд ашигладаг. Жишээ болгон [`RCTAlertManager`](https://github.com/facebook/react-native/blob/master/React/Modules/RCTAlertManager.m) гэснийг харна уу. Хэрэв callback-ыг хэзээ ч ажиллуулахгүй бол зарим санах ой нь алдагдана. Хэрэв  `onSuccess` болон `onFail` callback-ууд дамжсан бол та аль нэгийг нь л дуудаж ажиллуулах нь зүйтэй. 

Хэрэв та алдаа юм шиг объектыг  JavaScript руу дамжуулах бол [`RCTUtils.h`](https://github.com/facebook/react-native/blob/master/React/Base/RCTUtils.h)-аас `RCTMakeError`-ыг ашиглаарай.
Одоогоор энэ нь JavaScript руу алдаа бүхий dictionary-ыг дамжуулж байгаа ч бид үүнийг автоматаар бодит JavaScript `Error` объектыг цаашид дамжуулдаг болгохоор зорьж байгаа. 

## Promises

Натив модуль promise гүйцэтгэдэг. Тиймдээ ч таны кодыг хялбарчилна. Ялангуяа ES2016-ын `async/await` синтакс ашиглаж байгаа үед. Холбоотой натив методын сүүлийн параметрууд нь  `RCTPromiseResolveBlock` , `RCTPromiseRejectBlock` байхад холбогдох JS метод нь JS Promise объект руу буцдаг.

Callback-ын оронд promise ашиглахаар дээрх кодыг өөрчилбөл:

```objectivec
RCT_REMAP_METHOD(findEvents,
                 findEventsWithResolver:(RCTPromiseResolveBlock)resolve
                 rejecter:(RCTPromiseRejectBlock)reject)
{
  NSArray *events = ...
  if (events) {
    resolve(events);
  } else {
    NSError *error = ...
    reject(@"no_events", @"There were no events", error);
  }
}
```

Энэхүү методын JavaScript хэсэг нь Promise-т очно.  Энэ нь юу гэсэн үг вэ гэхээр дараалал бүхий функц дотроо та `await` түлхүүр үгийг ашиглан дуудан, үр дүнг нь хүлээж болно гэсэн үг:

```javascript
async function updateEvents() {
  try {
    var events = await CalendarManager.findEvents();

    this.setState({events});
  } catch (e) {
    console.error(e);
  }
}

updateEvents();
```

## Threading

Натив модуль нь ямар салбар процесс дээр дуудагдаж байгаа тухай ямар нэг ойлголт авах учиргүй. React Native нь натив модулийн методыг тусдаа цурвал GCD дарааллаар дууддаг. Гэхдээ энэ нь ажиллагааны нэг хэсэг бөгөөд өөрчлөгдөх магадлалтай. `- (dispatch_queue_t)methodQueue`  метод нь натив модуль методуудаа ямар дарааллаар ажиллуулах вэ гэдгийг зааж өгөх боломж олгодог. Жишээлбэл, хэрэв зөвхөн thread дээр байх iOS API ашиглах хэрэгтэй бол ингэнэ:

```objectivec
- (dispatch_queue_t)methodQueue
{
  return dispatch_get_main_queue();
}
```

Үүний нэгэн адил ажиллагаа удаад байвал натив модуль нь блок хийх хэрэггүй бөгөөд ажиллах дарааллаа тодорхойлох учиртай. Жишээ нь `RCTAsyncLocalStorage` модуль нь өөрийн дарааллыг үүсгэдэг тул дискны хандалтыг удаашруулан React-ын дарааллыг блок хийдэггүй:

```objectivec
- (dispatch_queue_t)methodQueue
{
  return dispatch_queue_create("com.facebook.React.AsyncLocalStorageQueue", DISPATCH_QUEUE_SERIAL);
}
```


 `methodQueue`-т юу гэж тодорхойлж өгнө тэр нь таны модулийн бүх методод хамаатай. Хэрэв  таны методуудаас _зөвхөн нэг_нь удаа н ажиллаад байвал (эсвэл ямар нэг шалтгаанаар бусдаас өөр дараалал дээр ажиллах хэрэгтэй бол), та метод дотроо `dispatch_async` ашиглан тухайн нэг методын кодыг бусдад нь нөлөөлүүлэхгүйгээр өөр дараалалд ажиллуулж болно:

```objectivec
RCT_EXPORT_METHOD(doSomethingExpensive:(NSString *)param callback:(RCTResponseSenderBlock)callback)
{
  dispatch_async(dispatch_get_global_queue(DISPATCH_QUEUE_PRIORITY_DEFAULT, 0), ^{
    // Call long-running code on background thread
    ...
    // You can invoke callback from any thread/queue
    callback(@[...]);
  });
}
```

> **ТЭМДЭГЛЭЛ**: Модуль хооронд илгээх дарааллыг хуваалцах
>
>  Модуль эхлэх үед  `methodQueue` метод дуудагдана. Тэгээд bridge хүлээн авах болохоор модуль дотроо ашиглах гээгүй л бол дарааллыг тогтоох шаардлагагүй. Гэхдээ та олон модулиудыг нэг дараалал байлгахыг хүсвэл тус бүр нь нэг дарааллаар дуудагдаад, буцаж байгаа эсэхийг нягтлах хэрэгтэй. Нэг нэр бүхий дараалалд буцдаг байх нь хангалтгүй юм. 

## Dependency Injection

Bridge нь бүртгэл бүхий бүх  RCTBridgeModules-ыг автоматаар эхлүүлдэг. Гэхдээ та өөрийн модуль instance-аа ажиллуулахыг хүсэж болно (хамаарал бүхий функц ажиллуулах жишээ нь).

Та RCTBridgeDelegate Protocol-ыг ажиллуулах класс үүсгэж үүнийг хийнэ. RCTBridge-ыг делегатын хамт аргумент хэлбэрээр эхлүүлэн, эхний bridge-тэй RCTRootView ажиллуулна. 

```objectivec
id<RCTBridgeDelegate> moduleInitialiser = [[classThatImplementsRCTBridgeDelegate alloc] init];

RCTBridge *bridge = [[RCTBridge alloc] initWithDelegate:moduleInitialiser launchOptions:nil];

RCTRootView *rootView = [[RCTRootView alloc]
                        initWithBridge:bridge
                            moduleName:kModuleName
                     initialProperties:nil];
```

## Constant (Тогтмол) экспорт хийх

Натив модуль нь Javascript ажиллах хугацаанд тэр дороо бэлэн байх constant-уудыг экспорт хийдэг. Тогтмол өгөгдөл бүхий мэдээлэл солилцоход энэ нь тустай. 

```objectivec
- (NSDictionary *)constantsToExport
{
  return @{ @"firstDayOfTheWeek": @"Monday" };
}
```

JavaScript нь уг утгыг шууд зэрэгцэн ашиглаж чадна:

```javascript
console.log(CalendarManager.firstDayOfTheWeek);
```

Constant-ууд нь эхлэх үед л экспорт хийгдэж байгаа гэдгийг санаарай. Ажиллаж эхлэх үед  `constantsToExport` утгыг өөрчилбөл Javascript-ын орчинд нөлөөлөхгүй. 

### Implementing `+ requiresMainQueueSetup`

Хэрэв та `- constantsToExport` дарж тодорхойлох юм бол та `+ requiresMainQueueSetup`-ыг ашиглан таны модуль гол thread дээр эхэлнэ гэдгийг React Native-т мэдэгдэх хэрэгтэй. Эс бөгөөс анхааруулга гарч ирэх бөгөөд `+ requiresMainQueueSetup` ашиглахгүй бол цаашдаа модуль чинь ар хэсэгт эхлээд байх болно:

```objectivec
+ (BOOL)requiresMainQueueSetup
{
  return YES;  // only do this if your module initialization relies on calling UIKit!
}
```

Хэрэв модуль чинь UIKit хандахыг шаардахгүй бол та  `+ requiresMainQueueSetup`-т `NO` гэсэн хариу өгөх нь зүйтэй.


### Enum Constants

`NS_ENUM`-ын Enum-уудыг эхлээд RCTConvert-т өргөтгөхгүйгээр метод аргументаар ашиглаж болохгүй. 

Дараах `NS_ENUM` тодорхойлолтыг экспорт хийхийн тулд:

```objectivec
typedef NS_ENUM(NSInteger, UIStatusBarAnimation) {
    UIStatusBarAnimationNone,
    UIStatusBarAnimationFade,
    UIStatusBarAnimationSlide,
};
```
Та RCTConvert-ын класс өргөтгөлийг ингэж үүсгэх ёстой:

```objectivec
@implementation RCTConvert (StatusBarAnimation)
  RCT_ENUM_CONVERTER(UIStatusBarAnimation, (@{ @"statusBarAnimationNone" : @(UIStatusBarAnimationNone),
                                               @"statusBarAnimationFade" : @(UIStatusBarAnimationFade),
                                               @"statusBarAnimationSlide" : @(UIStatusBarAnimationSlide)}),
                      UIStatusBarAnimationNone, integerValue)
@end
```
Тэгээд та методуудаа тодорхойлж, enum constant-уудаа ингэж экспорт хийнэ:

```objectivec
- (NSDictionary *)constantsToExport
{
  return @{ @"statusBarAnimationNone" : @(UIStatusBarAnimationNone),
            @"statusBarAnimationFade" : @(UIStatusBarAnimationFade),
            @"statusBarAnimationSlide" : @(UIStatusBarAnimationSlide) };
};

RCT_EXPORT_METHOD(updateStatusBarAnimation:(UIStatusBarAnimation)animation
                                completion:(RCTResponseSenderBlock)callback)
```

Экспортлосон метод руу чинь дамжуулагдахаас өмнө байгаа selector ашиглан enum нь автоматаар unwrap хийгддэг (дээрх жишээ дээр бол `integerValue`).

## Эвентийг JavaScript руу илгээх

Натив модуль нь шууд дуудахгүйгээр Javascript-т эвентийн дохио өгч чаддаг. `RCTEventEmitter` дэд класс хийн, `supportedEvents`-ыг ажиллуулан `self sendEventWithName`-ыг дуудах нь хамгийн зүйтэй арга нь юм:

```objectivec
// CalendarManager.h
#import <React/RCTBridgeModule.h>
#import <React/RCTEventEmitter.h>

@interface CalendarManager : RCTEventEmitter <RCTBridgeModule>

@end
```

```objectivec
// CalendarManager.m
#import "CalendarManager.h"

@implementation CalendarManager

RCT_EXPORT_MODULE();

- (NSArray<NSString *> *)supportedEvents
{
  return @[@"EventReminder"];
}

- (void)calendarEventReminderReceived:(NSNotification *)notification
{
  NSString *eventName = notification.userInfo[@"name"];
  [self sendEventWithName:@"EventReminder" body:@{@"name": eventName}];
}

@end
```

JavaScript код нь шинэ `NativeEventEmitter` үүсгэн эдгээр эвентийн талаар мэдээллийг хүлээн авч чадна. 

```javascript
import { NativeEventEmitter, NativeModules } from 'react-native';
const { CalendarManager } = NativeModules;

const calendarManagerEmitter = new NativeEventEmitter(CalendarManager);

const subscription = calendarManagerEmitter.addListener(
  'EventReminder',
  (reminder) => console.log(reminder.name)
);
...
// Don't forget to unsubscribe, typically in componentWillUnmount
subscription.remove();
```

 JavaScript руу эвент илгээх нэмэлт жишээ харахыг хүсвэл [`RCTLocationObserver`](https://github.com/facebook/react-native/blob/master/Libraries/Geolocation/RCTLocationObserver.m) гэснийг уншина уу.

### Optimizing for zero listeners

Хэрэв эвентийн мэдээллийг хүлээн авах юу ч байхгүй байхад ямар ч шаардлагагүй эвент үүсгэн өргөтгөх юм бол та анхааруулга хүлээн авна. Үүнээс зайлсхийхийн тулд модулийнхаа ажлын ачааллыг оновчтой тодорхойлж өгөх хэрэгтэй (жишээ нь upstream-ын мэдээллийг хүлээн авахаа болиулах эсвэл арын даалгаврыг түр зогсоох). Та  `RCTEventEmitter` дэд класс дотроо `startObserving`, `stopObserving`-ыг дарж тодорхойлж болно.  

```objectivec
@implementation CalendarManager
{
  bool hasListeners;
}

// Will be called when this module's first listener is added.
-(void)startObserving {
    hasListeners = YES;
    // Set up any upstream listeners or background tasks as necessary
}

// Will be called when this module's last listener is removed, or on dealloc.
-(void)stopObserving {
    hasListeners = NO;
    // Remove upstream listeners, stop unnecessary background tasks
}

- (void)calendarEventReminderReceived:(NSNotification *)notification
{
  NSString *eventName = notification.userInfo[@"name"];
  if (hasListeners) { // Only send events if anyone is listening
    [self sendEventWithName:@"EventReminder" body:@{@"name": eventName}];
  }
}
```

## Swift экспорт хийх

Swift нь макро дэмждэггүй учир React Native-тай ашиглахын тулд бага зэрэг тохиргоо хийх шаардлагатай. Ажиллахын хувьд бол бараг ялгаагүй. 

Бидэн адилхан `CalendarManager` Swift классаар байлаа гэж бодъё:

```swift
// CalendarManager.swift

@objc(CalendarManager)
class CalendarManager: NSObject {

  @objc(addEvent:location:date:)
  func addEvent(name: String, location: String, date: NSNumber) -> Void {
    // Date is ready to use!
  }

  @objc
  func constantsToExport() -> [String: Any]! {
    return ["someKey": "someValue"]
  }

}
```

> **ТЭМДЭГЛЭЛ**:  Objective-C ажиллах эхлэх үед класс, функцууд зөв экспортлогдсон эсэхийг шалгах зорилгоор @objc modifiers ашиглах нь чухал. 

Тэгээд ажиллуулах хувийн файл үүсгэнэ. Энэ нь шаардлагатай мэдээллийг React Native bridge-т өгөх юм:

```objectivec
// CalendarManagerBridge.m
#import <React/RCTBridgeModule.h>

@interface RCT_EXTERN_MODULE(CalendarManager, NSObject)

RCT_EXTERN_METHOD(addEvent:(NSString *)name location:(NSString *)location date:(nonnull NSNumber *)date)

@end
```

Swift, Objective-C-т анхлан суралцаж байгаа хүмүүст хэлэхэд, [iOS төсөлд хоёр хэл хольж хэрэглэх бол](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/BuildingCocoaApps/MixandMatch.html), Objective-C файлуудыг Swift-д өгөхийн тулд танд нэмэлт холбох файл буюу bridging header хэрэгтэй. 

Та `File>New File`  цэсийг ашиглан Xcode-ооор аппдаа Swift файл нэмэх бол Xcode нь энэхүү header file-ыг үүсгэхэд тусална. 

```objectivec
// CalendarManager-Bridging-Header.h
#import <React/RCTBridgeModule.h>
```

Та мөн модулийнхаа Javascript нэрийг өөрчлөх эсвэл экспорт хийж буй методуудынхаа нэрийг өөрчлөхийг хүсвэл  `RCT_EXTERN_REMAP_MODULE`,  `_RCT_EXTERN_REMAP_METHOD` ашиглаж болно.
Нэмэлт мэдээллийг [`RCTBridgeModule`](https://github.com/facebook/react-native/blob/master/React/Base/RCTBridgeModule.h) дээрээс харна уу.

> **Гуравдагч талын модуль үүсгэх үед анхаарах зүйлс**: 
Swift кодтой статик сангуудыг Xcode 9 болон шинэ хувилбарууд нь дэмждэг. iOS статик санг модульд оруулан Swift ашиглах үед Xcode төсөл хийхдээ таны гол апп төсөл чинь Swift код, bridging header-ыг агуулсан байх учиртай. Хэрэв апп хийх төсөлд чинь Swift код байхгүй бол нэг арга нь дан хоосон .swift файл болон хоосон bridging header үүсгэх юм. 

