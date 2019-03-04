### roadrunner
---
https://github.com/spiral/roadrunner

```php
<?php
ini_set('display_errors', 'stderr');
include "vendor/autoload.php";

$relay = new Spiral\Goridge\StreamRelay(STDIN, STDOUT);
$psr7 = new Spiral\RoadRunner\PSR7Client(new Spiral\RoadRunner\Worker($relay));

while ($req = $psr7->acceptRequest()) {
  try {
    $resp = new \Zend\Diactors\Response();
    $resp->getBody()->write("hello world");
    
    $psr7->respond($resp);
  } catch (\Throwable $e) {
    $psr7->getWorker()->error((string)$e);
  }
}

>
```

```
http:
  address: 0.0.0.0:8080
  workers:
    command: "php psr-worker.php"
    pool:
      numWorkers: 4
```

```
```


