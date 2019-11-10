# fawry-node [![Build Status](https://travis-ci.com/fawry-api/fawry-node.svg?branch=master)](https://travis-ci.com/fawry-api/fawry-node) [![codecov](https://codecov.io/gh/fawry-api/fawry-node/badge.svg?branch=master)](https://codecov.io/gh/fawry-api/fawry-node?branch=master)


## Install

The module depends on http module as a peer dependency.
In the future it will be pluggable with:

  - [x] [axios](https://github.com/axios/axios)
  - [ ] [request](https://github.com/request/request)
  - [ ] [superagent](https://github.com/visionmedia/superagent)
  - [ ] [got](https://github.com/sindresorhus/got)
  - [ ] [node-fetch](https://github.com/bitinn/node-fetch)

Please make sure to add to your project one of the supported above modules.

```
$ npm install fawry-node
```


## Usage

```js
const fawry = require('fawry-node');

/*
  params: config * for details check contracts/init.js
  does: leverages JS closure to initialize a Fawry instance with common configration
  return: {
    request // http client instance you could intercept, transform do whatever the http module supports
    charge,
    refund,
    status
  }
*/
const fawryClient = fawry.init({
  isSandbox: true,
  fawrySecureKey: '<fawry_secure_key>'
});


/*
  params: data * for details check contracts/charge.js
  does: sends a post request with your valid fawry options to the /charge endpint
  return: Promise
*/

fawryClient.charge({
  merchantCode: '<merchant_code>',
  merchantRefNum: 'io5jxf3jp27kfh8m719arcqgw7izo7db',
  customerProfileId: 'ocvsydvbu2gcp528wvl64i9z5srdalg5',
  customerMobile: '012345678901',
  paymentMethod: 'PAYATFAWRY',
  currencyCode: 'EGP',
  amount: 17.20,
  description: 'the charge request description',
  chargeItems: [{
    itemId: 'fk3fn9flk8et9a5t9w3c5h3oc684ivho',
    description: 'desc',
    price: 17.20,
    quantity: 1
  }]
});

/*
  params: data * for details check contracts/refund.js
  does: sends a post request with your valid fawry options to the /refund endpint
  return: Promise
*/

fawryClient.refund({
  merchantCode: '<merchant_code>',
  referenceNumber: '931337410',
  refundAmount: 81.13
});

/*
  params: params * for details check contracts/status.js
  does: sends a get request with your valid fawry options to the /status endpint
  return: Promise
*/

fawryClient.status({
  merchantCode: '<merchant_code>',
  merchantRefNumber: 'ssshxb98phmyvm434es62kage3nsm2cj'
});
```
