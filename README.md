# BoltIoT API wrapper

## A tiny and simple but useful utility library for fetching BoltIoT Cloud API.

-  Supports every part of currently documented Bolt Cloud API(and Bolt Cloud Pro API)
-  No dependancies, only single .js file
-  It uses fetch API and async await under the hood, polyfill required for older browsers

## How to Use

-  Import it with cdn or directly

```
https://cdn.jsdelivr.net/gh/RoneelV/BoltIoT-fetch-wrapper/index.js
```

-  Set API token and device name with setKey
   (The following script will automatically set them when you upload code on Bolt cloud)

```javascript
setKey('{{ApiKey}}', '{{Name}}')
```

-  You can use any functions now :tada:

```javascript
try {
   let response = await analogRead('A0')
   myElement.innerText = response
} catch (e) {
   console.error(e.name + ' : ' + e.message)
}
```

## API

-  Name of functions are exactly same as the name of respective commands. [check out Bolt Cloud API](https://docs.boltiot.com/docs/introduction)
-  Every function has device_name as last and optional parameter for checking another devices without ever having setKey again.
-  'Multi' functions will accept lists of numbers as argument(like pins, values) and will return Promise that return a list of numbers.
-  Read functions will return Promises that return the read value as string.
-  Write functions will return Promises that return the written value. (would be the same as the one provided as argument)
-  In general, every function will return every property(except "success" and with the same name and order) that is returned by the respective command, if number of properties is >1, the function will return an object with them. (in a Promise)
-  In case of error / failure, the function will return an object with name and message as properties.

```javascript
// Reading state of a pin
digitalMultiRead(pins)
   .then(console.log)
   .catch(console.error)
// Writing state
myElem.onclick = async e => {
   try {
      let response = await servoWrite(pin, e.target.value)
      myDisplayElem.innerText = 'Successfully changed value of ..'
   } catch (er) {
      myDisplayElem.innerText = e.name + ' : ' + e.message
   }
}
// Utilies
restart()
   .then(/*Do something*/)
   .catch(/*Do something*/)
```
