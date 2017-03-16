### 常用js片段

1、输入数字和小数点
```
$(".only_num").keyup(function(){     
    var tmptxt=$(this).val();     
    $(this).val(tmptxt.replace(/[^\d.]/g,''));     
}).bind("paste",function(){     
    var tmptxt=$(this).val();     
    $(this).val(tmptxt.replace(/[^\d.]/g,''));     
}).css("ime-mode", "disabled");
```

2、checkbox全选和取消
```
$('input[name=item]').prop('checked', true);  // 选中
$('input[name=item]').prop('checked', false); // 取消

ps：attr('check', true)不好用
```