![image_squidhome@2x.png](http://i.imgur.com/RIvu9.png) 

# sails-memory

Tested with Sails 0.9

## Extract from my bootstrap.test.js
This populates barrels with the fixtures, saves the states and then saves the state restoring it before running each test

```js
var setupFixtures = _.once(() => new Promise(function (resolve) {
  barrels.populate([
    'centres',
    'subjects',
    'movement',
    'detainee',
    'event',
    'heartbeat',
    'prebooking',
    'bed',
    'bedevent',
    'port'
  ], function (err) {
    if (err) throw err;
    Sails.adapters['sails-memory-restorable'].saveState('test');
    resolve();
  });

}));


module.exports = {
  beforeEach: () => setupFixtures()
      .then(() => {
        Sails.adapters['sails-memory-restorable'].restoreState('test');
      });
  }
};

```


An in-memory object store which works great as a bundled, starter database (with the strict caveat that it is for non-production use only).

## About Sails.js
http://sailsjs.com

## About Waterline
Waterline is a new kind of storage and retrieval engine.  It provides a uniform API for accessing stuff from different kinds of databases, protocols, and 3rd party APIs.  That means you write the same code to get users, whether they live in mySQL, LDAP, MongoDB, or Facebook.

[![githalytics.com alpha](https://cruel-carlota.pagodabox.com/a22d3919de208c90c898986619efaa85 "githalytics.com")](http://githalytics.com/balderdashy/sails-dirty)
