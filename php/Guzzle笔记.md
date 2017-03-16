### Guzzle笔记

    参考文档：http://docs.guzzlephp.org/en/latest/overview.html
    
1、composer安装

```
{
   "require": {
      "guzzlehttp/guzzle": "~6.0"
   }
}
```

2、多请求并行
```
use GuzzleHttp\Client;
use GuzzleHttp\Promise;

$client = new Client();

// Initiate each request but do not block
$promises = [
    'req1' => $client->getAsync('http://api.test.com/req1'),
    'req2' => $client->getAsync('http://api.test.com/req2')
];

// Wait for the requests to complete, even if some of them fail
$results = Promise\settle($promises)->wait();

// You can access each result using the key provided to the unwrap
// function.
echo $results['req1']->getHeader('Content-Length');
echo $results['req2']->getHeader('Content-Length');
```

3、并行请求拿结果
```
$requests = function() use ($comm_ids) {
    $base_url = APF::get_instance()->get_config('broker_basic_url');
    foreach ($comm_ids as $comm_id) {
        $url = $base_url . 'broker/commSignTopSigner/?is_nocheck=1&commId=' . $comm_id;
        yield new GuzzleHttp\Psr7\Request('GET', $url);
    }
};

方法一：
$responses = [];
$pool = new GuzzleHttp\Pool(new GuzzleHttp\Client(), $requests(), [
    'concurrency' => 5,
    'fulfilled' => function ($response, $index) use (&$responses, $comm_ids) {
        $responses[$index] = $response;
    },
    'rejected' => function ($reason, $index) use (&$responses, $comm_ids) {
        $responses[$index] = [];
    },
]);

$pool->promise()->wait();

// 输出response集合
foreach ($responses as $response) {
    $response->getBody()->getContents()
}


方法二：
$container = [];
$stack = GuzzleHttp\HandlerStack::create();
$stack->push(GuzzleHttp\Middleware::history($container));
$client = new GuzzleHttp\Client(['handler' => $stack]);
$pool = new GuzzleHttp\Pool($client, $requests(), ['concurrency' => 5]);
$pool->promise()->wait();

foreach ($container as $transaction) {
    parse_str($transaction['request']->getUri()->getQuery(), $query);
    print_r($query);
    print_r($transaction['response']->getBody()->getContents());
}
```

3、POST请求
```
// 根据不同的Content-Type生成对应的stream

// application/json
$stream = GuzzleHttp\Psr7\stream_for('{"a":"1", "b":"2"}');

// application/x-www-form-urlencoded
$stream = GuzzleHttp\Psr7\stream_for('a=1&b=2');

$header = [
    'Content-Type' => 'application/x-www-form-urlencoded',
];

$url = 'xxx';

$request = new \GuzzleHttp\Psr7\Request('POST', $url, $header, $stream);
```