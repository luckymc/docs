### getimagesize

```
> print_r(getimagesize('/Users/chengl/Downloads/mnjpg.jpg'));
Array
(
    [0] => 2250         // 宽
    [1] => 1500         // 高
    [2] => 3            // 类型
    [3] => width="2250" height="1500"
    [bits] => 8
    [mime] => image/png
)

$imageTypeArray = array(
    0 => 'UNKNOWN',
    1 => 'GIF',
    2 => 'JPEG',
    3 => 'PNG',
    4 => 'SWF',
    5 => 'PSD',
    6 => 'BMP',
    7 => 'TIFF_II',
    8 => 'TIFF_MM',
    9 => 'JPC',
    10 => 'JP2',
    11 => 'JPX',
    12 => 'JB2',
    13 => 'SWC',
    14 => 'IFF',
    15 => 'WBMP',
    16 => 'XBM',
    17 => 'ICO',
    18 => 'COUNT'  
);


图片上传，以jpeg类型为例

$old_image = imagecreatefromjpeg($image_url);
$new_image = imagecreatetruecolor($width, $height);

imagecopy($new_image, $old_image, 0, 0, $x1, $y1, $width, $height);

ob_start();
imagejpeg($new_image);
$contents = ob_get_contents();
ob_end_clean();

imagedestroy($old_image);
imagedestroy($new_image);

// 新图片上传到图片服务器
$url = APF::get_instance()->get_config('image_upload_url');
$client = Apf_Http_CurlClient::getInstance();
$ret = $client->doPost($url, array('file' => base64_encode($contents)), array(), array(), 1000);
$ret = json_decode($ret, true);
```