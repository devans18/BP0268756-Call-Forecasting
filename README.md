# 




<h1 align="center"> BP0268756-Call-Forecasting </h1> <br>
<p align="center">
<!--   <a href="https://gitpoint.co/">
    <img alt="GitPoint" title="GitPoint" src="http://i.imgur.com/VShxJHs.png" width="450">
  </a> 
</p>

<p align="center">
  GitHub in your pocket. Built with React Native.
</p>

<p align="center">
  <a href="https://itunes.apple.com/us/app/gitpoint/id1251245162?mt=8">
    <img alt="Download on the App Store" title="App Store" src="http://i.imgur.com/0n2zqHD.png" width="140">
  </a>

  <a href="https://play.google.com/store/apps/details?id=com.gitpoint">
    <img alt="Get it on Google Play" title="Google Play" src="http://i.imgur.com/mtGRPuM.png" width="140">
  </a> -->
</p>

Hello and welcome to this git. It is being used to support the development of a call forecasting model as part of a DTS apprenticeship completed through BPP.

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
## Table of Contents

- [Introduction](#introduction)
- [Background](#background)
- [Data Diagram](#data-diagram)
- [High Level Methodology](#high-level-methodology)
<!-- - [Contributors](#contributors)
- [Build Process](#build-process)
- [Backers](#backers-)
- [Sponsors](#sponsors-)
- [Acknowledgments](#acknowledgments) --!>

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## Introduction

Currently, workforce planning for the contact centre requires manual manipulation of forecasts issued by an antiquated system. It is resource intensive and requires a team of strategic forecasters to accurately predict customer contact volumes, and as a consequence, provide resource to address these. 
This project looks to use machine learning to produce an accurate base forecast that requires minimal adjustment, if any, to suit the needs of the business and customers. This solution will be created in python using the Facebook Prophet **insert link to FB Prophet github** which is a powerful LSTM forecasting model allowing for manipulation and cleansing within the model.

## Background 

What is resource planning
Why is it important
What methods are currently used - especially in Finance
What is machine learning
What are the benefits
How do we marry machine learning and forecasting - LSTM
How will this be applicable to the current issue
What do we hope to achieve

## Data Diagram

![image](https://github.com/user-attachments/assets/32690ffd-8735-4be1-a17c-01223ba29eeb)

## High Level Methodology

A customer calls in to the company. This call is handled by our IVR (Interactive Voice Response) system to help funnel a customer's request.
This IVR is part of the wider CCC (Cloud Contact Cisco platform), which handles and routes the customers call. From the customers perspective, they will call the main number, be filtered through the IVR and then placed in a queue to speak to an agent. This routing is handled by CCC. 

There are then three systems that the customer's data flows through:
1. Finess, which allows a call agent to speak to the customer **find details on Finess and reference**
2. Verint, which handles call recording and provides basic metrics about the call **find details on Verint and reference**
3. VIM, which captures further metrics about the calls and stores these in a large database **find details on VIM and reference**

Currently, the resource planning team uses Verint to provide a base forecast, which the wider planning team then use to make manual manipulations in Excel, before issuing to the scheduling team to arrange work rotas and shift coverage. The current base forecast has a resolution of daily.

Instead, by extracting the raw performance metrics from VIM, data can be collected to a resolution of 15 minute intervals, allowing for the base forecast to look at intraday forecasting, rather than daily forecasting. 

There is an existing business process that extracts the data from VIM, and places it into a PowerBI tool called TOMI (Telephony Operational MI), which allows for data to be saved in .xlsx format in quarterly chunks. This data can then be re-merged into one continuous dataset, which currently runs back as far as 01/01/2023. 
_A proposition to both append the data and provide base analytic insight into the raw data has been created in another PowerBI dashboard, however there is scope, should the major project work, to incorporate this into the main solution. _
Another dataset is created to represent holidays which have skewed the base data, as well as another dataset which will be used to replace raw data with null entries where there has been an unplanned event (incident/IT outtage/news event) which has caused an unexpected change in customer behaviour which is unlikely to be repeated or unable to be forecasted again.

These datasets then fed into a Facebook Prophet based model that will be used to create a future forecast. The most optimal time period to forecast is **define best forecast and discuss why with references. talk about inaccuracies in future forecasts due to the potential in wholescale changes in customer behaviour. Perhaps 2 weeks is appropriate**

Old forecasts will be reviewed against performance, and the model tweaked where appropriate



<!-- View repository and user information, control your notifications and even manage your issues and pull requests. Built with React Native, GitPoint is one of the most feature-rich unofficial GitHub clients that is 100% free.

**Available for both iOS and Android.**

<p align="center">
  <img src = "http://i.imgur.com/HowF6aM.png" width=350>
</p>

## Features

A few of the things you can do with GitPoint:

* View user activity feed
* Communicate on your issue and pull request conversations
* Close or lock issues
* Apply labels and assignees
* Review and merge pull requests
* Create new issues
* Star, watch and fork repositories
* Control your unread and participating notifications
* Easily search for any user or repository

<p align="center">
  <img src = "http://i.imgur.com/IkSnFRL.png" width=700>
</p>

<p align="center">
  <img src = "http://i.imgur.com/0iorG20.png" width=700>
</p>

## Feedback

Feel free to send us feedback on [Twitter](https://twitter.com/gitpointapp) or [file an issue](https://github.com/gitpoint/git-point/issues/new). Feature requests are always welcome. If you wish to contribute, please take a quick look at the [guidelines](./CONTRIBUTING.md)!

If there's anything you'd like to chat about, please feel free to join our [Gitter chat](https://gitter.im/git-point)!

## Contributors

This project follows the [all-contributors](https://github.com/kentcdodds/all-contributors) specification and is brought to you by these [awesome contributors](./CONTRIBUTORS.md).

## Build Process

- Follow the [React Native Guide](https://facebook.github.io/react-native/docs/getting-started.html) for getting started building a project with native code. **A Mac is required if you wish to develop for iOS.**
- Clone or download the repo
- `yarn` to install dependencies
- `yarn run link` to link react-native dependencies
- `yarn start:ios` to start the packager and run the app in the iOS simulator (`yarn start:ios:logger` will boot the application with [redux-logger](<https://github.com/evgenyrodionov/redux-logger>))
- `yarn start:android` to start the packager and run the app in the the Android device/emulator (`yarn start:android:logger` will boot the application with [redux-logger](https://github.com/evgenyrodionov/redux-logger))

Please take a look at the [contributing guidelines](./CONTRIBUTING.md) for a detailed process on how to build your application as well as troubleshooting information.

**Development Keys**: The `CLIENT_ID` and `CLIENT_SECRET` in `api/index.js` are for development purposes and do not represent the actual application keys. Feel free to use them or use a new set of keys by creating an [OAuth application](https://github.com/settings/applications/new) of your own. Set the "Authorization callback URL" to `gitpoint://welcome`.

## Backers [![Backers on Open Collective](https://opencollective.com/git-point/backers/badge.svg)](#backers)

Thank you to all our backers! 🙏 [[Become a backer](https://opencollective.com/git-point#backer)]

<a href="https://opencollective.com/git-point#backers" target="_blank"><img src="https://opencollective.com/git-point/backers.svg?width=890"></a>

## Sponsors [![Sponsors on Open Collective](https://opencollective.com/git-point/sponsors/badge.svg)](#sponsors)

Support this project by becoming a sponsor. Your logo will show up here with a link to your website. [[Become a sponsor](https://opencollective.com/git-point#sponsor)]

<a href="https://opencollective.com/git-point/sponsor/0/website" target="_blank"><img src="https://opencollective.com/git-point/sponsor/0/avatar.svg"></a>
<a href="https://opencollective.com/git-point/sponsor/1/website" target="_blank"><img src="https://opencollective.com/git-point/sponsor/1/avatar.svg"></a>
<a href="https://opencollective.com/git-point/sponsor/2/website" target="_blank"><img src="https://opencollective.com/git-point/sponsor/2/avatar.svg"></a>
<a href="https://opencollective.com/git-point/sponsor/3/website" target="_blank"><img src="https://opencollective.com/git-point/sponsor/3/avatar.svg"></a>
<a href="https://opencollective.com/git-point/sponsor/4/website" target="_blank"><img src="https://opencollective.com/git-point/sponsor/4/avatar.svg"></a>
<a href="https://opencollective.com/git-point/sponsor/5/website" target="_blank"><img src="https://opencollective.com/git-point/sponsor/5/avatar.svg"></a>
<a href="https://opencollective.com/git-point/sponsor/6/website" target="_blank"><img src="https://opencollective.com/git-point/sponsor/6/avatar.svg"></a>
<a href="https://opencollective.com/git-point/sponsor/7/website" target="_blank"><img src="https://opencollective.com/git-point/sponsor/7/avatar.svg"></a>
<a href="https://opencollective.com/git-point/sponsor/8/website" target="_blank"><img src="https://opencollective.com/git-point/sponsor/8/avatar.svg"></a>
<a href="https://opencollective.com/git-point/sponsor/9/website" target="_blank"><img src="https://opencollective.com/git-point/sponsor/9/avatar.svg"></a>

## Acknowledgments

Thanks to [JetBrains](https://www.jetbrains.com) for supporting us with a [free Open Source License](https://www.jetbrains.com/buy/opensource). --!>
