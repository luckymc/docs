### Nginx笔记

* 重新request_uri
```
# /anjuke/4.0 => /4.0
location /anjuke/4.0 {
    if ($request_uri ~* /anjuke/4.0/(.+)\?(.*)) {
        set $u $1;
        set $p $2;
        rewrite .* /4.0/$u?$p;
        proxy_pass http://10.249.6.129;
    }
}
```