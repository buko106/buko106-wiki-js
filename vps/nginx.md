<!-- TITLE: Nginx -->
<!-- SUBTITLE: Nginx周りの設定 -->

# やったこと
* wiki.buko106.tokyo のサブドメインをVPSの設定で追加
* /etc/nginx/conf.d/wiki.confの編集

```apache_conf
server {
    listen 80;
    listen [::]:80;
    server_name wiki.buko106.tokyo;

    location / {
        proxy_set_header Host $http_host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_pass http://127.0.0.1:(ポート番号);
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_next_upstream error timeout http_502 http_503 http_504;
    }
}
```

* 自分用のファイルを置くためのサブドメインを切って、サブディレクトリを設置
	* rewriteでリダイレクトしたり、root変えたり、index.htmlを隠蔽できるようにtry_filesなどなど