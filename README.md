Angular DDP Client
==================

How to use
----------

Include the script in your HTML:
```
<script src="path_to_file/angular-ddp.js"></script>
```

Then connect:

```
angular.module('starter.controllers', ['angularDDP'])

.controller('SampleCtrl', function($scope, $timeout, DDP) {

  var ddp = new DDP('ws://localhost:3000/websocket');
  var ddpconnect = ddp.connect();

  ddpconnect.then(function() {
    ddp.subscribe('api_products_latest', [0,5])
      .then(function() {
        $timeout(function () {
          $scope.products = ddp.getCollection('products');
          console.log($scope.products);
        });
      });
    ddp.watch('products', function(changedDoc, message) {
      // Something
    });
  });

});
```
