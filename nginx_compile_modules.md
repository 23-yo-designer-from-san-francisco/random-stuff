Before starting, you will need to install some dependencies required to compile Nginx in your system. You can install all of them with the following command:

apt-get install dpkg-dev build-essential gnupg2 git gcc cmake libpcre3 libpcre3-dev zlib1g zlib1g-
dev openssl libssl-dev curl unzip -y
Once all the packages are installed, you can proceed to the next step.

Step 3 – Add Nginx Repository
Next, you will need to add the Nginx official repository to download the latest version of the Nginx source.

First, import the Nginx GPG key with the following command:

curl -L https://nginx.org/keys/nginx_signing.key | apt-key add -
Next, add the Nginx repository with the following command:

nano /etc/apt/sources.list.d/nginx.list
Add the following lines:

deb http://nginx.org/packages/ubuntu/ focal nginx
deb-src http://nginx.org/packages/ubuntu/ focal nginx
Save and close the file when you are finished. Next, update the repository with the following command:

apt-get update -y
Once your repository is updated, you can proceed to the next step.

Step 4 – Install Nginx with Brotli Support
First, download the latest version of the Nginx source with the following command:

cd /usr/local/src
apt-get source nginx
Next, install the required dependencies to build Nginx:

apt-get build-dep nginx -y
Next, download the latest version of Brotli from the Git repository using the following command:

git clone --recursive https://github.com/google/ngx_brotli.git
Next, change the directory to the Nginx source and edit the rules file:

cd /usr/local/src/nginx-*/
nano debian/rules
Find the ‘config.env.nginx‘ and ‘config.env.nginx_debug’ section and add the following line within ./configure line:

--add-module=/usr/local/src/ngx_brotli
Save and close the file, then compile and build the nginx package with the following command:

dpkg-buildpackage -b -uc -us
The above command will generate Nginx .deb files inside /usr/local/src directory.

You can list them with the following command:

ls /usr/local/src/*.deb
You should see both files in the following output:

/nginx_1.18.0-2~focal_amd64.deb nginx-dbg_1.18.0-2~focal_amd64.deb
Next, install the Nginx by running the both *.deb file:

dpkg -i /usr/local/src/*.deb
Step 5 – Configure Nginx to Use Brotli
Next, you will need to configure Nginx to use Brotli module. You can do it by editing the Nginx main configuration file:

nano /etc/nginx/nginx.conf
Add the following lines inside the http { section:

brotli on;
brotli_comp_level 6;
brotli_static on;
brotli_types text/plain text/css application/javascript application/x-javascript text/xml 
application/xml application/xml+rss text/javascript image/x-icon 
image/vnd.microsoft.icon image/bmp image/svg+xml;
Save and close the file, then verify the Nginx for any syntax errors:

nginx -t
You should get the following output:

nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful
Next, start the Nginx service using the following command:

systemctl start nginx
You can verify the status of the Nginx service with the following command:

systemctl status nginx
You should get the following output:

nginx.service - nginx - high performance web server
Loaded: loaded (/lib/systemd/system/nginx.service; enabled; vendor preset: enabled)
Active: active (running) since Sat 2020-10-31 06:29:17 UTC; 3s ago
Docs: http://nginx.org/en/docs/
Process: 21451 ExecStart=/usr/sbin/nginx -c /etc/nginx/nginx.conf (code=exited,
status=0/SUCCESS)
Main PID: 21452 (nginx)
Tasks: 2 (limit: 4691)
Memory: 1.7M
CGroup: /system.slice/nginx.service
├─21452 nginx: master process /usr/sbin/nginx -c /etc/nginx/nginx.conf
└─21453 nginx: worker process
Oct 31 06:29:17 ubuntu2004 systemd[1]: Starting nginx - high performance web server...
Oct 31 06:29:17 ubuntu2004 systemd[1]: Started nginx - high performance web server.
Step 6 – Verify Brotli Module
At this point, Nginx is installed and configured with Brotli support. Now, verify whether the Brotli module is enabled or not by running the following command:

curl -H 'Accept-Encoding: br' -I http://localhost
You should get the “Content-Encoding: br” in the following output:

HTTP/1.1 200 OK
Server: nginx/1.18.0
Date: Sat, 31 Oct 2020 06:30:24 GMT
Content-Type: text/html
Last-Modified: Tue, 21 Apr 2020 14:09:01 GMT
Connection: keep-alive
ETag: W/"5e9efe7d-264"
Content-Encoding: br
