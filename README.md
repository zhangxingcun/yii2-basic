Yii 2 Basic 带有登录和权限管理
============================

yii2的基础模版没有用户登录和权限管理部分,每次创建新的项目都需要从头开始,很烦人所以
整理一下发布出来,方便自己也方便他人.

说明:

	1)用户登录采用自己创建模型进行管理,在项目应用中,用户基本都需要增加很多属性,而且
	也参与各种业务流程.网上虽然有封装,但是用着总是别扭.参考
	https://github.com/linuor/digpage
	整理一个基本用户模型,在实际应用中根据自己的项目再进行修改.推荐一下,linuor的教程
	非常不错
	
	2)权限管理采用 https://github.com/mdmsoft/yii2-admin
	权限采用文件存储,放在/rbac目录，注意需要开放读写权限

	3)可以打包下载，包含所有插件

	4)如果无法访问或文件不存在，请检查访问权限

安装:

	1)克隆
	git clone git@github.com:zhangxingcun/yii2-basic
	
	2)可以不用,安装失败时再运行	
	composer global require fxp/composer-asset-plugin dev-master
	
	3)部署	
	cd yii2-basic
	composer update 
	
	4)配置参数,主要是数据库
	
	5)数据库迁移
	yii migrate
	如果使用admin的菜单,需要迁移
	yii migrate --migrationPath=@mdm/admin/migrations
	
	6)创建第一个用户,默认为管理员.后续用户需要配置
	yii init/user
	
	----------------------------------------
	web.php
	'as access' => [
	    'class' => 'mdm\admin\components\AccessControl',
	    'allowActions' => [
		'admin/*', //open
		'site/*',
	    ]
	],

	7)进入权限管理 http://127.0.0.1/basic/web/index.php?r=admin
	给第一个用户超级权限

	8)关闭admin权限
	web.php
	'as access' => [
	    'class' => 'mdm\admin\components\AccessControl',
	    'allowActions' => [
		//'admin/*', //close
		'site/*',
	    ]
	],
