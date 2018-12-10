php

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

vue-cli

配置代理：修改 config/index.js

```js
module.exports = {

//...
dev: {
    // Paths
    assetsSubDirectory: 'static',
    assetsPublicPath: '/',
    proxyTable: {
      '/api': {
        target: 'http://localhost/',
        changeOrigin: true,
        pathRewrite: {
          '^/api': ''   //重写接口
        }
      }
    },
// ...
```

集中管理 api, 并封装 axios

/src/api

```
|-- src
    |-- api
        |-- demo
            |-- index.js
        |-- fetch.js
        |-- index.js
```

/src/api/fetch.js

```js
import axios from 'axios'

const instance = axios.create({
})

export default instance
```

/src/api/index.js

```js
export * from './demo'
```

/src/api/demo/index.js

```js
import fetch from '@/api/fetch'
import qs from 'qs';

export function GetTestList (param) {
    return fetch.get('/api/getTestList.php', qs.stringify(param))
}
```

demo 组件

```
//...
<ul>
    <li v-for="(item, index) in list" :key="index">{{ item.content }}</li>
</ul>
// ...

import {
    GetTestList
} from '@/api'

data () {
    return {
        list: []
    }
},

created () {
    this.getTestList()
},

methods: {

    getTestList () {
        GetTestList().then(res => {
            if (res) {
                this.list = res.data.list
            }
        }).catch(err => {
            console.log(err.message)
        })
    },

}

```
