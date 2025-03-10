
<img align="left" width="56" height="56" src="https://user-images.githubusercontent.com/6492229/98982291-70b42480-251f-11eb-8d67-4b0b1b6e917b.png"> react-native-paper-dates
---
<br>

<p float="left">
<img src="https://badgen.net/bundlephobia/minzip/react-native-paper-dates" />
<img src="https://badgen.net/npm/dy/react-native-paper-dates" />
<img src="https://badgen.net/npm/types/react-native-paper-dates" />
<img src="https://badgen.net/npm/license/react-native-paper-dates" />
<img src="https://img.shields.io/badge/Runs%20with%20Expo-4630EB.svg?style=flat-square&logo=EXPO&labelColor=f3f3f3&logoColor=000" />
</p>

- Smooth and fast cross platform Material Design **date** picker and **time** picker for ([react-native-paper](https://callstack.github.io/react-native-paper/))
- Tested on Android, iOS and the web
- Uses the native Date.Intl API's which work out of the box on the web / iOS (automatic day name, month translations without bundle size increase)
- For Android Intl support please follow the [android-caveats guide](https://github.com/web-ridge/react-native-paper-dates#android-caveats)
- Simple API
- Typesafe
- Endless (virtual) scrolling
- Performant
- Great React Native Web support
- No dependencies outside of ([react-native-paper](https://callstack.github.io/react-native-paper/))

[![Demo of react-native-paper-dates](https://user-images.githubusercontent.com/6492229/98866767-bd3f2780-246d-11eb-890e-3491b47c95c5.gif)](https://www.youtube.com/watch?v=SHhQU2doTug)

View video in better frame [on YouTube](https://www.youtube.com/watch?v=SHhQU2doTug)

Web demo: [reactnativepaperdates.com](http://reactnativepaperdates.com/)

## About us
We want developers to be able to build software faster using modern tools like GraphQL, Golang and React Native.

Give us a follow on Twitter:
[RichardLindhout](https://twitter.com/RichardLindhout),
[web_ridge](https://twitter.com/web_ridge)

## Donate
Instead of spending all your money on a M1 Mac, give it to us so we can buy one.

[Donate with PayPal](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=7B9KKQLXTEW9Q&source=url)


## Getting started

Yarn
```
yarn add react-native-paper-dates
```

npm
```
npm install react-native-paper-dates --save
```


## Usage

### Single date Picker

```tsx
import * as React from 'react';
import { Button } from 'react-native-paper';
import { DatePickerModal } from 'react-native-paper-dates';

export default function ReadMeExampleSingle() {
  const [date, setDate] = React.useState<Date | undefined>(undefined);
  const [open, setOpen] = React.useState(false);

  const onDismissSingle = React.useCallback(() => {
    setOpen(false);
  }, [setOpen]);

  const onConfirmSingle = React.useCallback(
    (params) => {
      setOpen(false);
      setDate(params.date);
    },
    [setOpen, setDate]
  );

  return (
    <>
      <Button onPress={() => setOpen(true)} uppercase={false} mode="outlined">
        Pick single date
      </Button>
      <DatePickerModal
        // locale={'en'} optional, default: automatic
        mode="single"
        visible={open}
        onDismiss={onDismissSingle}
        date={date}
        onConfirm={onConfirmSingle}
        // validRange={{
        //   startDate: new Date(2021, 1, 2),  // optional
        //   endDate: new Date(), // optional
        // }}
        // onChange={} // same props as onConfirm but triggered without confirmed by user
        // saveLabel="Save" // optional
        // label="Select date" // optional
        // animationType="slide" // optional, default is 'slide' on ios/android and 'none' on web
      />
    </>
  );
}
```

### Range picker
```tsx
import * as React from 'react';
import { Button } from 'react-native-paper';

import { DatePickerModal } from 'react-native-paper-dates';

export default function ReadMeExampleRange() {
  const [range, setRange] = React.useState<{
    startDate: Date | undefined;
    endDate: Date | undefined;
  }>({ startDate: undefined, endDate: undefined });

  const [open, setOpen] = React.useState(false);

  const onDismiss = React.useCallback(() => {
    setOpen(false);
  }, [setOpen]);

  const onConfirm = React.useCallback(
    ({ startDate, endDate }) => {
      setOpen(false);
      setRange({ startDate, endDate });
    },
    [setOpen, setRange]
  );

  return (
    <>
      <Button onPress={() => setOpen(true)} uppercase={false} mode="outlined">
        Pick range
      </Button>
      <DatePickerModal
        // locale={'en'} optional, default: automatic
        mode="range"
        visible={open}
        onDismiss={onDismiss}
        startDate={range.startDate}
        endDate={range.endDate}
        onConfirm={onConfirm}
        // validRange={{
        //   startDate: new Date(2021, 1, 2),  // optional
        //   endDate: new Date(), // optional
        // }}
        // onChange={} // same props as onConfirm but triggered without confirmed by user
        // locale={'nl'} // optional
        // saveLabel="Save" // optional
        // label="Select period" // optional
        // startLabel="From" // optional
        // endLabel="To" // optional
        // animationType="slide" // optional, default is slide on ios/android and none on web
      />
    </>
  );
}

```


### Multiple dates picker
```tsx
import * as React from 'react';
import { Button } from 'react-native-paper';

import { DatePickerModal } from 'react-native-paper-dates';

export default function ReadMeExampleMultiple() {
  const [dates, setDates] = React.useState<Date[] | undefined>();
  const [open, setOpen] = React.useState(false);

  const onDismiss = React.useCallback(() => {
    setOpen(false);
  }, [setOpen]);

  const onConfirm = React.useCallback((params) => {
    setOpen(false);
    setDates(params.dates);
    console.log('[on-change-multi]', params);
  }, []);

  return (
    <>
      <Button onPress={() => setOpen(true)} uppercase={false} mode="outlined">
        Pick multiple dates
      </Button>

      <DatePickerModal
        // locale={'en'} optional, default: automatic
        mode="multiple"
        visible={open}
        onDismiss={onDismiss}
        dates={dates}
        onConfirm={onConfirm}
        // validRange={{
        //   startDate: new Date(2021, 1, 2),  // optional
        //   endDate: new Date(), // optional
        // }}
        // locale={'nl'} // optional
        // saveLabel="Save" // optional
        // label="Select period" // optional
        // startLabel="From" // optional
        // endLabel="To" // optional
        // animationType="slide" // optional, default is slide on ios/android and none on web
      />
    </>
  );
}
```

### Time picker
```tsx
import * as React from 'react'
import { Button } from 'react-native-paper'
import { TimePickerModal } from 'react-native-paper-dates'

export default function TimePickerPage() {
  const [visible, setVisible] = React.useState(false)
  const onDismiss = React.useCallback(() => {
    setVisible(false)
  }, [setVisible])

  const onConfirm = React.useCallback(
    ({ hours, minutes }) => {
      setVisible(false);
      console.log({ hours, minutes });
    },
    [setVisible]
  );


  return (
    <>
      <TimePickerModal
        visible={visible}
        onDismiss={onDismiss}
        onConfirm={onConfirm}
        hours={12} // default: current hours
        minutes={14} // default: current minutes
        label="Select time" // optional, default 'Select time'
        cancelLabel="Cancel" // optional, default: 'Cancel'
        confirmLabel="Ok" // optional, default: 'Ok'
        animationType="fade" // optional, default is 'none'
        locale={'en'} // optional, default is automically detected by your system
      />
      <Button onPress={()=> setVisible(true)}>
        Pick time
      </Button>
    </>
  )
}
```






## Roadmap
Things on our roadmap have labels with `enhancement`.
https://github.com/web-ridge/react-native-paper-dates/issues

## Tips & Tricks
- Use 0.14+ version of React-Native-Web (Modal and better number input)
- Try to avoid putting the Picker Modals inside of a scrollView
If that is **not possible** use the following props on the surrounding ScrollViews/Flatlists

```javascript
    keyboardDismissMode="on-drag"
    keyboardShouldPersistTaps="handled"
    contentInsetAdjustmentBehavior="always"
```
This is to prevent the need to press 2 times before save or close button in modal works (1 press for closing keyboard, 1 press for confirm/close)
[React Native Issue: #10138](https://github.com/facebook/react-native/issues/10138)

## Android Caveats

You will need to add a polyfill for the Intl API on Android if:

- You have [Hermes](https://github.com/facebook/hermes/issues/23) enabled
- You have [Hermes](https://github.com/facebook/hermes/issues/23) disabled and you want to support locales outside of en-US and you don't have the org.webkit:android-jsc-intl:+ variant enabled in your app/build.gradle

Install polyfills with Yarn

```
yarn add react-native-localize @formatjs/intl-pluralrules @formatjs/intl-getcanonicallocales @formatjs/intl-listformat @formatjs/intl-displaynames @formatjs/intl-locale @formatjs/intl-datetimeformat @formatjs/intl-numberformat @formatjs/intl-relativetimeformat
```

or npm

```
npm install react-native-localize @formatjs/intl-pluralrules @formatjs/intl-getcanonicallocales @formatjs/intl-listformat @formatjs/intl-displaynames @formatjs/intl-locale @formatjs/intl-datetimeformat @formatjs/intl-numberformat @formatjs/intl-relativetimeformat --save
```

In your app starting entrypoint e.g. `./index.js` or even better use a `index.android.js` to prevent importing on iOS/web put the following code. (don't forget to import the languages you want to support, in the example only english language is supported)

```javascript
// on top of your index.android.js file
const isAndroid = require('react-native').Platform.OS === 'android';
const isHermesEnabled = !!global.HermesInternal;

// in your index.js file
if (isHermesEnabled || isAndroid) {

  require('@formatjs/intl-getcanonicallocales/polyfill');
  require('@formatjs/intl-locale/polyfill');


  require('@formatjs/intl-pluralrules/polyfill');
  require('@formatjs/intl-pluralrules/locale-data/en.js'); // USE YOUR OWN LANGUAGE OR MULTIPLE IMPORTS YOU WANT TO SUPPORT

  require('@formatjs/intl-displaynames/polyfill');
  require('@formatjs/intl-displaynames/locale-data/en.js'); // USE YOUR OWN LANGUAGE OR MULTIPLE IMPORTS YOU WANT TO SUPPORT

  require('@formatjs/intl-listformat/polyfill');
  require('@formatjs/intl-listformat/locale-data/en.js'); // USE YOUR OWN LANGUAGE OR MULTIPLE IMPORTS YOU WANT TO SUPPORT

  require('@formatjs/intl-numberformat/polyfill');
  require('@formatjs/intl-numberformat/locale-data/en.js'); // USE YOUR OWN LANGUAGE OR MULTIPLE IMPORTS YOU WANT TO SUPPORT

  require('@formatjs/intl-relativetimeformat/polyfill');
  require('@formatjs/intl-relativetimeformat/locale-data/en.js'); // USE YOUR OWN LANGUAGE OR MULTIPLE IMPORTS YOU WANT TO SUPPORT

  require('@formatjs/intl-datetimeformat/polyfill');
  require('@formatjs/intl-datetimeformat/locale-data/en.js'); // USE YOUR OWN LANGUAGE OR MULTIPLE IMPORTS YOU WANT TO SUPPORT

  require('@formatjs/intl-datetimeformat/add-golden-tz.js');



  // https://formatjs.io/docs/polyfills/intl-datetimeformat/#default-timezone
  let RNLocalize = require('react-native-localize');
  if ('__setDefaultTimeZone' in Intl.DateTimeFormat) {
    Intl.DateTimeFormat.__setDefaultTimeZone(RNLocalize.getTimeZone());
  }
}
```

## Contributing

See the [contributing guide](CONTRIBUTING.md) to learn how to contribute to the repository and the development workflow.

## License

MIT


### Checkout our other libraries
- Smooth and fast cross platform Material Design Tabs for React Native Paper: [react-native-paper-tabs](https://github.com/web-ridge/react-native-paper-tabs)
- Simple translations in React (Native): [react-ridge-translations](https://github.com/web-ridge/react-ridge-translations)
- Simple global state management in React (Native): [react-ridge-state](https://github.com/web-ridge/react-ridge-state)
- 1 command utility for React Native (Web) project: [create-react-native-web-application](https://github.com/web-ridge/create-react-native-web-application)
