# Laravel 小程序图文海报生成包

微信小程序中生成朋友圈分享图文海报的一种解决方案

[![Build Status](https://travis-ci.org/ibrandcc/laravel-miniprogram-poster.svg?branch=master)](https://travis-ci.org/ibrandcc/laravel-miniprogram-poster)
[![Scrutinizer Code Quality](https://scrutinizer-ci.com/g/ibrandcc/laravel-miniprogram-poster/badges/quality-score.png?b=master)](https://scrutinizer-ci.com/g/ibrandcc/laravel-miniprogram-poster/?branch=master)
[![Code Coverage](https://scrutinizer-ci.com/g/ibrandcc/laravel-miniprogram-poster/badges/coverage.png?b=master)](https://scrutinizer-ci.com/g/ibrandcc/laravel-miniprogram-poster/?branch=master)
[![Build Status](https://scrutinizer-ci.com/g/ibrandcc/laravel-miniprogram-poster/badges/build.png?b=master)](https://scrutinizer-ci.com/g/ibrandcc/laravel-miniprogram-poster/build-status/master)

## Featrue

1. 基于html可实现复杂的文字，图片，阴影效果。 
2. 清晰度和文件大小合理
3. 使用简单、即插即用

## TODO：

1. 存储 Model 对象和图片对应关系，避免重复生成图片。

## 体验

扫码进入商品详情页分享生成图文体验

![iBrand开源体验店](https://iyoyo.oss-cn-hangzhou.aliyuncs.com/post/miniprogramcode/1.jpg)

### 安装
```
composer require ibrand/laravel-miniprogram-poster 
```
- 低于 Laravel5.5 版本，`config/app.php` 文件中 'providers' 添加`iBrand\Poster\PhantoMmagickServiceProvider::class`

- 图片保存在  `storage/app/public` 下所以需要执行  `php artisan storage:link`

- 如需自定义配置请执行 `php artisan vendor:publish --provider="iBrand\Poster\PhantoMmagickServiceProvider" --tag="config"`

### 配置项

``` 
    return [
    	//图片存储位置
    	'disks'      => [
    		'MiniProgramShare' => [
    			'driver'     => 'local',
    			'root'       => storage_path('app/public/share'),
    			'url'        => env('APP_URL') . '/storage/share',
    			'visibility' => 'public',
    		],
    	],
    	//图片宽度
    	'width'      => '575px',
    	//放大倍数
    	'zoomfactor' => 1.5,
    	//0-100,100质量最高
    	'quality'    => 100,
    	//是否压缩图片
    	'compress'   => true,
    ];
```

### 使用
```
use iBrand\Miniprogram\Poster\MiniProgramShareImg;
    
$url = 'https://www.ibrand.cc/';
$result = MiniProgramShareImg::generateShareImage($url);

```
返回结果：
```
    [
        'url'  => 'http://xxx.png',   图片访问url
        'path' => 'path/to/image', 图片文件路径
    ]
```
### 字体安装

如果需要实现复杂的字体效果，需要安装字体，比如在 centos 上就没有微软雅黑的字体，所以如果生成的图片有指定的特殊字体，需要在服务器上进行安装。

* window 将下载的字体文件复制到C:Windows\Fonts目录下或者双击字体文件进行安装
* mac 下载的字体文件 双击字体文件进行安装
* centos
```
# 安装微软雅黑
wget -P /tmp/ https://iyoyo.oss-cn-hangzhou.aliyuncs.com/mirror/fonts/msyh.ttf
wget -P /tmp/ https://iyoyo.oss-cn-hangzhou.aliyuncs.com/mirror/fonts/msyhbd.ttf
wget -P /tmp/ https://iyoyo.oss-cn-hangzhou.aliyuncs.com/mirror/fonts/msyhl.ttf
cd /usr/share/fonts/lyx/
mkdir chinese
cd chinese
mv /tmp/msyhbd.ttf ./
chmod 755 *.ttf
yum -y install mkfontscale
mkfontscale
mkfontdir
fc-cache -fv
```

### Resource

项目基于[PhantomMagick](https://github.com/anam-hossain/phantommagick)
