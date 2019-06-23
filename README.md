# Create a Static Page  on S3 AWS behind Nginx As reverse proxy

This configuration is very simple, I will show you as configure a static page on AWS S3 Bucket

## Create a bucket S3 on AWS

Very images below:

![Image01](https://raw.githubusercontent.com/renizgo/nginxtos3/master/images/image01.png)
Image01

![Image02](https://raw.githubusercontent.com/renizgo/nginxtos3/master/images/image02.png)
Image02

![Image03](https://raw.githubusercontent.com/renizgo/nginxtos3/master/images/image03.png)
Image03

![Image04](https://raw.githubusercontent.com/renizgo/nginxtos3/master/images/image04.png)
Image04

![Image05](https://raw.githubusercontent.com/renizgo/nginxtos3/master/images/image05.png)
Image05

![Image06](https://raw.githubusercontent.com/renizgo/nginxtos3/master/images/image06.png)
Image06

![Image07](https://raw.githubusercontent.com/renizgo/nginxtos3/master/images/image07.png)
Image07

## Configure your Nginx

One simple configuration with Nginx via Docker container

```
docker build -t renizgo/nginx-to-s3 .
```

Run docker image generated above

```
docker run -d -p 80:80 renizgo/nginx-to-s3
```

Configure your ```/ect/hosts```, insert line below:

```
127.0.0.1  renatomarigo.com.br
```

## Just configuration set

```
    server_name renatomarigo.com.br;

    #charset koi8-r;
    #access_log  /var/log/nginx/host.access.log  main;

    location / {
        proxy_set_header Host 'nginxtos3.s3-website-sa-east-1.amazonaws.com';
        proxy_set_header Authorization '';
        proxy_hide_header x-amz-id-2;
        proxy_hide_header x-amz-request-id;
        proxy_hide_header Set-Cookie;
        proxy_ignore_headers "Set-Cookie";
        proxy_intercept_errors on;
        proxy_pass http://nginxtos3.s3-website-sa-east-1.amazonaws.com/; # Edit your Amazon S3 Bucket name
        expires 1y;
        log_not_found off;
    }
```

## Access your site

http://renatomarigo.com.br

![Image08](https://raw.githubusercontent.com/renizgo/nginxtos3/master/images/image08.png)
Image08