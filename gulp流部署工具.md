gulp 流部署工具

安装

`cnpm i --save-dev gulp gulp-sftp`

在根目录下创建 `gulpfile.js` 文件

```
    const gulp = require('gulp')
    const ftp = require('gulp-sftp')
    
    const deployConfig = {
        dev: {
            remotePath: xxx, //远程路径
            host: xxx, // 主机地址
            user: xxx, // 登录名
            pass: xxx, // 密码
            port: '' // 端口
        },
        test: {
            remotePath: xxx,
            host: xxx,
            user: xxx,
            pass: xxx,
            port: ''
        },
        publicPath: '/dist/' // 要部署的文件目录
    }
    // 为安全起见，deployConfig 配置可以另新建文件，在上传远程库中忽略
    
    gulp.task('deploy:dev', function (callback) {
        console.log('正在部署开发环境')
        gulp.src('.' + deployConfig.publicPath + '**')
            .pipe(ftp(Object.assign({}, deployConfig.dev, {callback})))
    })
    
    gulp.task('deploy:test', function (callback) {
        console.log('正在部署测试环境')
        gulp.src('.' + deployConfig.publicPath + '**')
            .pipe(ftp(Object.assign({}, deployConfig.test, {callback})))
    })
    
    gulp.task('deploy:all', ['deploy:dev', 'deploy:test'])
    
    // 也可添加到 npm script 命令中
    
    "scripts": {
        "deploy:dev": "gulp deploy:dev",
        "deploy:test": "gulp deploy:test",
        "deploy:all": "gulp deploy:all"
    },
```