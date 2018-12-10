目录

```
|-- src
    |-- jquery.js
    |-- template-web.js
|-- getTestList.php
|-- test.php
```

getTestList.php

```php
<?php
    // 设置字符集
    header("Content-type=text/html;charset=utf-8;");

    $db_host = "localhost";
    $db_user = "root";
    $db_pw = "root";
    $db_name = "test";

    $conn = mysqli_connect($db_host, $db_user, $db_pw, $db_name);

    if (!$conn) die("数据库连接失败：".mysqli_connect_error());

    // echo "数据库连接成功";

    $sql = "select * from list";

    $result = mysqli_query($conn, $sql);

    $respoents = array();

    if (!$result) {
        $respoents['success'] = false;
    } else {
        $respoents['success'] = true;
        $respoents['list'] = array();
        while ($row = mysqli_fetch_assoc($result)) {
            array_push($respoents['list'], $row);
        }
    }

    // 释放结果集
    mysqli_free_result($result);
    // 关闭数据库
    mysqli_close($conn);
    // 输出 json 格式数据
    echo json_encode($respoents);
```

test.php

```php
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Test</title>
    <!-- 加载 jQuery -->
    <script src="src/jquery.js"></script>
    <!-- 加载 art-template：模板引擎 -->
    <script src="src/template-web.js"></script>
</head>
<body>
    
    <div id="listDiv"></div>

    <script id="listTemp" type="text/html">
        <ul>
            {{ each $data item }}
                <li>{{ item.content }}</li>
            {{ /each }}
        </ul>
    </script>

    <script>
        $(function() {

            $.ajax({
                type: "GET",
                url: "getTestList.php",
                data:{},
                dataType: "json",
                success: function(data) {
                    if (data.success && data.list.length) {
                        var html = template("listTemp", data.list);
                        $("#listDiv").html(html);
                    }
                },
                error: function(jqXHR, textStatus, errorThrown) {
                    alert(errorThrown)
                },
                complete: function() {
                    // success 和 error 都会执行
                }
            })

        })
    </script>

</body>
</html>
```