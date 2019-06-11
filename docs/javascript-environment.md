---
id: javascript-environment
title: JavaScript Орчин
---

## JavaScript ажиллах хугацаа

React Native ашиглахдаа та JavaScript кодоо хоёр орчинд ажиллуулна:

- Ихэнх тохиолдолд React Native нь [JavaScriptCore](http://trac.webkit.org/wiki/JavaScriptCore)-ыг ашиглана. 
Safari-ыг дэмждэг JavaScript хөдөлгүүр юм. iOS дээр бичиж болох санах ой байхгүй үед iOS дээр JavaScriptCore нь JIT ашигладаггүй. 

-  Chrome дибаг ашиглаж байгаа үед бүх JavaScript код нь Chrome дотроо ажиллах WebSockets-оор дамжуулан натив кодтойгоо харьцдаг. Chrome нь [V8](https://code.google.com/p/v8/)-ыг өөрийн JavaScript хөдөлгүүр болгон ашигладаг.

Хоёр орчин нь хоорондоо их төстэй ч зарим үл нийцсэн, харшлах зүйлс гардаг. Бид цаашдаа JavaScript-ын өөр хөдөлгүүр туршиж үзэж магадгүй байгаа. Тийм болохоор ажиллуулах хугацаанд хэт найдан, хамааралтай болох хэрэггүй. 

## JavaScript синтакс шилжүүлэгч

Бүр процесийг танихыг хүлээлгүй шинээр Javascript синтакс ашиглах боломжийг танд олгодог болохоор синтакс шилжүүлэгч нь код бичих ажлыг тааламжтай болгодог. 

React Native нь [Babel JavaScript compiler](https://babeljs.io)-ыг ашигладаг. Ямар шилжүүлэгчийг дэмждэг тухай [Babel documentation](https://babeljs.io/docs/plugins/#transform-plugins)-аас уншаарай.


React Native дээр ажиллах шилжүүлэгчийн тухай мэдээллийг [metro-react-native-babel-preset](https://github.com/facebook/metro/tree/master/packages/metro-react-native-babel-preset) гэснээс хараарай.

ES5

- Reserved Words: `promise.catch(function() { });`

ES6

- [Arrow functions](http://babeljs.io/docs/learn-es2015/#arrows): `<C onPress={() => this.setState({pressed: true})} />`
- [Block scoping](https://babeljs.io/docs/learn-es2015/#let-const): `let greeting = 'hi';`
- [Call spread](http://babeljs.io/docs/learn-es2015/#default-rest-spread): `Math.max(...array);`
- [Classes](http://babeljs.io/docs/learn-es2015/#classes): `class C extends React.Component { render() { return <View />; } }`
- [Constants](https://babeljs.io/docs/learn-es2015/#let-const): `const answer = 42;`
- [Destructuring](http://babeljs.io/docs/learn-es2015/#destructuring): `var {isActive, style} = this.props;`
- [for...of](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...of): `for (var num of [1, 2, 3]) {};`
- [Modules](http://babeljs.io/docs/learn-es2015/#modules): `import React, { Component } from 'react';`
- [Computed Properties](http://babeljs.io/docs/learn-es2015/#enhanced-object-literals): `var key = 'abc'; var obj = {[key]: 10};`
- [Object Concise Method](http://babeljs.io/docs/learn-es2015/#enhanced-object-literals): `var obj = { method() { return 10; } };`
- [Object Short Notation](http://babeljs.io/docs/learn-es2015/#enhanced-object-literals): `var name = 'vjeux'; var obj = { name };`
- [Rest Params](https://github.com/sebmarkbage/ecmascript-rest-spread): `function(type, ...args) {};`
- [Template Literals](http://babeljs.io/docs/learn-es2015/#template-strings): `` var who = 'world'; var str = `Hello ${who}`; ``

ES8

- [Function Trailing Comma](https://github.com/jeffmo/es-trailing-function-commas): `function f(a, b, c,) {};`
- [Async Functions](https://github.com/tc39/ecmascript-asyncawait): `async function doStuffAsync() { const foo = await doOtherStuffAsync(); };`

Үе 3

- [Object Spread](https://github.com/sebmarkbage/ecmascript-rest-spread): `var extended = { ...obj, a: 10 };`

Үе 1

- [Optional Chaining](https://github.com/tc39/proposal-optional-chaining): `var name = obj.user?.name;`

Тодорхой

- [JSX](https://reactjs.org/docs/jsx-in-depth.html): `<View style={{color: 'red'}} />`
- [Flow](http://flowtype.org/): `function foo(x: ?number): string {};`

## Polyfills

Javascript ажиллах хугацааг дэмждэг олон стандарт функцууд байдаг. 

Хөтөч

- [console.{log, warn, error, info, trace, table, group, groupEnd}](https://developer.chrome.com/devtools/docs/console-api)
- [CommonJS require](https://nodejs.org/docs/latest/api/modules.html)
- [XMLHttpRequest, fetch](network.md#content)
- [{set, clear}{Timeout, Interval, Immediate}, {request, cancel}AnimationFrame](timers.md#content)
- [navigator.geolocation](geolocation.md#content)

ES6

- [Object.assign](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/assign)
- String.prototype.{[startsWith](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/startsWith), [endsWith](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/endsWith), [repeat](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/repeat), [includes](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/includes)}
- [Array.from](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/from)
- Array.prototype.{[find](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/find), [findIndex](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/findIndex)}

ES7

- Array.prototype.{[includes](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/includes)}

ES8

- Object.{[entries](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/entries), [values](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/values)}

Specific

- `__DEV__`
