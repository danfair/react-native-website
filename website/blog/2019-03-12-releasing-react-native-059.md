---
title: Releasing React Native 0.59
author: Ryan Turner
authorTitle: Core Maintainer & React Native Developer
authorURL: https://twitter.com/turnrye
authorImageURL: https://avatars0.githubusercontent.com/u/701035?s=460&v=4
authorTwitter: turnrye
category: announcements
---

Welcome to the 0.59 release of React Native! This is another big release with 644 commits by 88 contributors. Contributions also come in other forms, so _thank you_ for maintaining issues, fostering communities, and teaching people about React Native. This month brings a number of highly anticipated changes, and we hope you enjoy them.

## 🎣 Hooks are here

React Hooks are part of this release, which let you reuse stateful logic across components. There is a lot of buzz about hooks, but if you haven't heard, take a look at some of the wonderful resources below:

> * [Introducing Hooks](https://reactjs.org/docs/hooks-intro.html) explains why we’re adding Hooks to React.
> * [Hooks at a Glance](https://reactjs.org/docs/hooks-overview.html) is a fast-paced overview of the built-in Hooks.
> * [Building Your Own Hooks](https://reactjs.org/docs/hooks-custom.html) demonstrates code reuse with custom Hooks.
> * [Making Sense of React Hooks](https://medium.com/@dan_abramov/making-sense-of-react-hooks-fdbde8803889) explores the new possibilities unlocked by Hooks.
> * [useHooks.com](https://usehooks.com/) showcases community-maintained Hooks recipes and demos.

Be sure to give this a try in your apps. We hope that you find the reuse as exciting as we do.

## 📱 Updated JSC means performance gains and 64-bit support on Android

React Native uses JSC ([JavaScriptCore](https://webkit.org/)) to power your application. JSC on Android was a few years old, which meant that a lot of modern JavaScript features weren't supported. Even worse, it performed poorly compared iOS's modern JSC. With this release, that all changes.

Thanks to some awesome work by [@DanielZlotin](https://github.com/danielzlotin), JSC has caught up with the past few years. This brings with it 64-bit support, modern JavaScript support, and [big performance improvements](https://github.com/react-native-community/jsc-android-buildscripts/tree/master/measure). Kudos to Daniel for also making this a maintainable process now so that we can take advantage of future WebKit improvements without so much legwork.

## 💨 Faster app launches with inline requires

We want to help people have performant React Native apps by default and are working to bring Facebook's optimizations to the community. Applications load resources as needed rather than slowing down launch. This feature is called "inline requires", as it lets Metro identify components to be lazy loaded. Apps with a deep and varied component architecture will see the most improvement.

![source of the `metro.config.js` file in the 0.59 template, demonstrating where to enable `inlineRequires`](/react-native/blog/assets/inline-requires.png)

We need the community to let us know how it works before we turn it on by default. When you upgrade to 0.59, there will be a new `metro.config.js` file; flip the options to true and give us [your feedback](https://twitter.com/hashtag/inline-requires)! Read more about inline requires [in the performance docs](https://facebook.github.io/react-native/docs/0.56/performance#inline-requires) to benchmark your app.

## 🚅 Lean core is underway

React Native is a large and complex project with a complicated repository. This makes the codebase less approachable to contributors, difficult to test, and bloated as a dev dependency. [Lean Core](https://github.com/react-native-community/discussions-and-proposals/issues/6) is our effort to address these issues by migrating code to separate libraries for better management. The past few releases have seen the first steps of this, but [let's get serious](https://www.youtube.com/watch?v=FMLKb4or8yg).

You may notice that additional components are now officially deprecated. This is great news, as there are now owners for these features actively maintaining them. Heed the warning messages and migrate to the new libraries for these features, because in they will be removed in a future release. Below is a table indicating the component, its status, and where you may migrate your use to.

| Component            | Deprecated? | New home                                                                                                                                                 |
| -------------------- | ----------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **AsyncStorage**     | 0.59        | [@react-native-community/react-native-async-storage](https://github.com/react-native-community/react-native-async-storage)                               |
| **ImageStore**       | 0.59        | [expo-file-system](https://github.com/expo/expo/tree/master/packages/expo-file-system) or [react-native-fs](https://github.com/itinance/react-native-fs) |
| **MaskedViewIOS**    | 0.59        | [@react-native-community/react-native-masked-view](https://github.com/react-native-community/react-native-masked-view)                                   |
| **NetInfo**          | 0.59        | [@react-native-community/react-native-netinfo](https://github.com/react-native-community/react-native-netinfo)                                           |
| **Slider**           | 0.59        | [@react-native-community/react-native-slider](https://github.com/react-native-community/react-native-slider)                                             |
| **ViewPagerAndroid** | 0.59        | [@react-native-community/react-native-viewpager](https://github.com/react-native-community/react-native-viewpager)                                       |

Over the coming months, there will be many more components following this path to a leaner core. We're looking for help with this &mdash; head over to the [lean core umbrella](https://github.com/facebook/react-native/issues/23313) to pitch in.

## 👩🏽‍💻 CLI improvements

React Native's command line tools are developer's entry point to the ecosystem, but they had long-standing issues and lacked official support. The CLI tools have been moved to a [new repository](https://github.com/react-native-community/react-native-cli), and a [dedicated group of maintainers](https://blog.callstack.io/the-react-native-cli-has-a-new-home-79b63838f0e6) have already made some exciting improvements.

Logs are formatted much better now. Commands now run nearly instantly &mdash; you'll immediately notice a difference:

![0.58's CLI is slow to start](/react-native/blog/assets/0.58-cli-speed.png)![0.58's CLI is nearly instantaneous](/react-native/blog/assets/0.59-cli-speed.png)

## 🔨 Breaking Changes

`react-native-git-upgrade` was outdated and troublesome, so we killed it. Please use `react-native upgrade` from now on. It makes use of [rn-diff-purge](https://github.com/react-native-community/rn-diff-purge) under the covers.

Android also was cleaned up according to Google's recommendations, which resulted in potential breakage of existing apps (presented as a runtime crash `You need to use a Theme.AppCompat theme (or descendant) with this activity.`). In `AndroidManifest.xml`, make sure that the `android:theme` value is an `AppCompat` theme like `@style/Theme.AppCompat.Light.NoActionBar`.

## 🤗 Thanks

Lots of new contributors helped with [enabling generation of native code from flow types](https://github.com/facebook/react-native/issues/22990) and [resolving Xcode warnings](https://github.com/facebook/react-native/issues/22609) - these are a great way to learn how Rect Native works and contributing to the greater good. Thank you! Look out for similar issues in the future.

While these are the highlights that we noted, there are many others to be excited about. To see all of the updates, take a look at the [changelog](https://github.com/react-native-community/react-native-releases/blob/master/CHANGELOG.md). 0.59 is a huge release – we can't wait for you to try it out.

We have even more improvements coming throughout the rest of the year. Stay tuned!

[Ryan](https://github.com/turnrye) and the whole [React Native core team](https://twitter.com/reactnative)
