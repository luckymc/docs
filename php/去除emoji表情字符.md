### 去除emoji表情字符

```
public function removeEmoji($clean_text)
{
    // 方法1：只取合法字符
    preg_match_all("/[\x{4e00}-\x{9fa5}|0-9|a-z|A-Z|_]/u", $clean_text, $matches);
    $clean_text = isset($matches[0]) ? implode('', $matches[0]) : '';


    // 方法2：去除表情字符，但测试过程中发现无法出去“国旗”表情
    // Match Emoticons
    $regexEmoticons = '/[\x{1F600}-\x{1F64F}]/u';
    $clean_text = preg_replace($regexEmoticons, '', $clean_text);

    // Match Miscellaneous Symbols and Pictographs
    $regexSymbols = '/[\x{1F300}-\x{1F5FF}]/u';
    $clean_text = preg_replace($regexSymbols, '', $clean_text);

    // Match Transport And Map Symbols
    $regexTransport = '/[\x{1F680}-\x{1F6FF}]/u';
    $clean_text = preg_replace($regexTransport, '', $clean_text);

    // Match Miscellaneous Symbols
    $regexMisc = '/[\x{2600}-\x{26FF}]/u';
    $clean_text = preg_replace($regexMisc, '', $clean_text);

    // Match Dingbats
    $regexDingbats = '/[\x{2700}-\x{27BF}]/u';
    $clean_text = preg_replace($regexDingbats, '', $clean_text);

    return $clean_text;
}
```