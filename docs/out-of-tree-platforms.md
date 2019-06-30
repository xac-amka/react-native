---
id: out-of-tree-platforms
title: Өөр гадны платформууд
---

React Native нь зөвхөн Android, iOS-т зориулагдсан зүйл биш. Бусад платформууд дээр ашиглах боломжтой, хамтын дэмжлэгтэйгээр хийгддэг төслүүд байдаг:

- [React Native Windows](https://github.com/Microsoft/react-native-windows) - Microsoft-ын Universal Windows Platform (UWP) болон Windows Presentation Foundation (WPF)-д зориулсан React Native үйлчилгээ
- [React Native DOM](https://github.com/vincentriemer/react-native-dom) - React Native-ын вэбд зориулсан туршилтын, цогц порт юм ([React Native Web](https://github.com/necolas/react-native-web)-тай бүү андуураарай. Зорилго нь өөр шүү)
- [React Native Turbolinks](https://github.com/lazaronixon/react-native-turbolinks) - Turbolinks 5 ашиглан хосолмол апп хийх зориулалттай React Native-ын тохируулагч.
- [React Native Desktop](https://github.com/status-im/react-native-desktop) - Qt-ын QML ашиглан React Native-ыг Desktop-т ашиглах боломжийг олгох зорилготой төсөл. [React Native Ubuntu](https://github.com/CanonicalLtd/react-native/) нь дахин засвар орохоо больсон системийн дуудалт юм.
- [React Native macOS](https://github.com/ptmt/react-native-macos) - macOS болон Cocoa-д зориулсан React Native-ын туршилтын системийн дуудалт юм.

## Өөрийн React Native платформ үүсгэх

Одоогоор React Native платформын бүр эхнээс нь хэрхэн үүсгэх тухай тийм ч их мэдээлэл байхгүй. Удахгүй гарах ([Fabric](https://facebook.github.io/react-native/blog/2018/06/14/state-of-react-native-2018))-ын нэг зорилго нь платформын ажлыг илүү хялбар болгох юм. 

### Нэгтгэх

React Native 0.57 дээр та өөрийн React Native платформыг React Native-ын JavaScript bundler болох [Metro](https://facebook.github.io/metro/)-ыг ашиглан бүртгүүлэх боломжтой. Энэ нь та `react-native bundle`-руу `--platform example`-ыг дамжуулж болно гэсэн үг. Ингэхээр `.example.js` гэсэн дагавартай Javascript файлуудыг хайж олно. 

Платформоо RNPM-т бүртгүүлэхийн тулд таны модулийн нэр нь эдгээрийн аль нэгтэй таарч байх учиртай:

- `react-native-example` - `react-native-` гэсэн топ модулиудыг хайна
- `@org/react-native-example` -  `react-native-` гэсэн ямар ч модулиудыг хайна
- `@react-native-example/module` -  `@react-native-` гэж эхэлсэн нэртэй ямар ч модулийг хайна

Та `package.json` дотроо үүнийг заавал оруулах ёстой:

```json
{
  "rnpm": {
    "haste": {
      "providesModuleNodeModules": ["react-native-example"],
      "platforms": ["example"]
    }
  }
}
```

`"providesModuleNodeModules"` нь модулиудын массив бөгөөд Haste модулийн хайлтын зам дээр нэмэгддэг.`"platforms"` нь платформуудын массив ба хүчин төгөлдөр байгаа платформ болж нэмэгдэнэ.

