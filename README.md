# fvtt_dnd5e_120
dnd5e系统1.2.0版本的备份

## 如何使用jsd帮助服务器上的fvtt加速 fvtt核心为0.7.9 5e版本1.2.0

在配置nginx环境中，配置文件对应位置添加如下内容，自行搜索位置

server
	{
	listen 80;
	# server_name xxxx.top; 按需求加 换成你的域名
	#ssl_certificate     C:\phpstudy_pro1\Extensions\Nginx1.16.1\ssl2\kagangtuya.top.crt; ssl配置区域，注释了
	#ssl_certificate_key C:\phpstudy_pro1\Extensions\Nginx1.16.1\ssl2\kagangtuya.top.key;
	client_max_body_size 300M;
	#location /scripts/foundry.js
	#{
	#rewrite '^(.*)$' 'https://cdn.jsdelivr.net/gh/kagangtuya-star/C-Learning_assignments@master/foundry.js' permanent;
	#}  这里选用，可能造成不稳定，启用可以增加大约5%的速度
	location  ^~ /systems/dnd5e/
	{
	rewrite '^/systems/dnd5e/(.*)$' 'https://cdn.jsdelivr.net/gh/kagangtuya-star/fvtt_dnd5e_120/dnd5e/$1' permanent;
	}
	location /{
	proxy_set_header Host $host;
	proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
	proxy_set_header X-Forwarded-Proto $scheme;
	proxy_set_header Upgrade $http_upgrade;
	proxy_set_header Connection "Upgrade";
	proxy_pass http://127.0.0.1:30000;
	}
}
