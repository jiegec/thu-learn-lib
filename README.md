# thu-learn2018-lib

This is a JavaScript library aimed to provide a program-friendly interface of [learn 2018 of Tsinghua University](https://leran2018.tsinghua.edu.cn).

This project is licensed under MIT License.

## Compatibility

The library uses `cross-fetch` and `real-isomorphic-fetch`, which provides cookie and redirection support in both browsers and JS engines (like node).

I don't like polyfill. In case of any problems, just upgrade your browser / Node.

## Installation

`npm install --save thu-learn2018-lib`

## Build from source

### Release version

`npm i && npm run build`

You can find the library in `lib/`.

### Test version

`npm i && npm run watch`

You can find the unpacked Chrome extension in `dist/`. Install it in Chrome and click the `t` icon in extension bar, then execute anything you want in the Console of Chrome Developer Tool. The helper class is attached as `window.Learn2018Helper` in this mode.

## Usage

```javascript
import { Learn2018Helper } from 'thu-learn2018-lib';

// in JS engines, each instance owns different cookie jars
const helper = new Learn2018Helper();

// all following methods are async

// first login
const loginSuccess = await helper.login('user', 'pass');

// get get semester info
const semester = await helper.getCurrentSemester();

// get courses of this semester
const courses = await helper.getCourseForSemester(semester.id);

// get detail information about the course
const discussions = await helper.getDiscussionList(courses.id);
const notifications = await helper.getNotificationList(courses.id);
const files = await helper.getFileList(courses.id);
const homework = await helper.getHomeworkList(courses.id);
const questions = await helper.getQuestionList(courses.id);

// logout if you want, has no effect in browsers
helper.logout();
```

In browsers, the class will be attached to `window.Learn2018Helper`.

According to security strategies (CORS, CORB) of browsers, you might need to run the code in the page context of `https://learn2018.tsinghua.edu.cn` and `https://id.tsinghua.edu.cn`. The simplest way is to run the code as a browser extension.

## Typing

See `lib/types.d.ts` for type definitions.