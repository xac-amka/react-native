---
id: native-modules-setup
title: Натив модулийг тохируулах
---

Натив модулиуд нь ихэвчлэн npm пакэжээр хүрдэг. Энгийн Javascript-аас гадна тэд нь платформ тус бүрийн натив код агуулсан байдаг. npm пакэжийн талаа дэлгэрэнгүй мэдэхийг хүсвэл [энэ зааврыг](https://docs.npmjs.com/getting-started/publishing-npm-packages) уншина уу.

Натив модулиуд нь 

Аливаа натив модульд зориулсан энгийн нэг төслийн бүтцийг тохируулан хийхийн тулд бид гуравдагч талын багажийг ашиглана [react-native-create-library](https://github.com/frostney/react-native-create-library). Тухайн сан хэрхэн ажилладаг тухай та лавшруулан судалж болно. Бидэнд харин ердөө энэ л хэрэгтэй:

```
$ npm install -g react-native-create-library
$ react-native-create-library MyLibrary
```

MyLibrary нь шинэ модулийн нэр нь байх юм. Үүний дараа та `MyLibrary` гэсэн фолдерыг олж, npm пакэжээ компьютертоо доорх командыг өгч суулгана:

```
$ npm install
```

Үүний дараа та гол react аппынхаа фолдер руу очоод (`react-native init MyApp` гэж үүсгэсэн)

- package.json дотроо шинээр үүсгэсэн модулиа dependency гэж нэмнэ
- `npm install` гэж өгөн, компьютер дээр npm сандаа зөөнө.

Үүний дараа та native-modules-ios эсвэл native-module-android руу код нэмэх боломжтой болно. Платформ тус бүрт зориулсан зааврыг  `MyLibrary` доторх README.md гэсэн хэсгэээс уншина уу. 
