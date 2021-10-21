Add brotli support to Nginx

[source](https://www.atlantic.net/dedicated-server-hosting/how-to-install-brotli-module-for-nginx-on-ubuntu-20-04/)

Step 1 – Install Required Dependencies
Before starting, you will need to install some dependencies required to compile Nginx in your system. You can install all of them with the following command:

```bash
apt-get install dpkg-dev build-essential gnupg2 git gcc cmake libpcre3 libpcre3-dev zlib1g zlib1g-
dev openssl libssl-dev curl unzip -y
```

Once all the packages are installed, you can proceed to the next step.

Step 2 – Add Nginx Repository
Next, you will need to add the Nginx official repository to download the latest version of the Nginx source.

First, import the Nginx GPG key with the following command:

```bash
curl -L https://nginx.org/keys/nginx_signing.key | apt-key add -
```
Next, add the Nginx repository with the following command:

```bash
nano /etc/apt/sources.list.d/nginx.list
```
Add the following lines:
```bash
deb http://nginx.org/packages/ubuntu/ focal nginx
deb-src http://nginx.org/packages/ubuntu/ focal nginx
```
Save and close the file when you are finished. Next, update the repository with the following command:

```bash
apt-get update -y
```
Once your repository is updated, you can proceed to the next step.

Step 3 – Install Nginx with Brotli Support
First, download the latest version of the Nginx source with the following command:

```bash
cd /usr/local/src
apt-get source nginx
```

Next, install the required dependencies to build Nginx:

```bash
apt-get build-dep nginx -y
```
Next, download the latest version of Brotli from the Git repository using the following command:

```bash
git clone --recursive https://github.com/google/ngx_brotli.git

```
Next, change the directory to the Nginx source and edit the rules file:

```bash
cd /usr/local/src/nginx-*/
nano debian/rules
```

Find the ‘config.env.nginx‘ and ‘config.env.nginx_debug’ section and add the following line within ./configure line:
`--add-module=/usr/local/src/ngx_brotli`
Save and close the file, then compile and build the nginx package with the following command:

```bash
dpkg-buildpackage -b -uc -us
```

The above command will generate Nginx .deb files inside /usr/local/src directory.

You can list them with the following command:

```bash
ls /usr/local/src/*.deb
```
You should see both files in the following output:

`/nginx_1.18.0-2~focal_amd64.deb nginx-dbg_1.18.0-2~focal_amd64.deb`
Next, install the Nginx by running the both *.deb file:

```bash
dpkg -i /usr/local/src/*.deb
```

Step 4 – Configure Nginx to Use Brotli
Next, you will need to configure Nginx to use Brotli module. You can do it by editing the Nginx main configuration file:

```bash
nano /etc/nginx/nginx.conf
```

Add the following lines inside the http { section:

`brotli on;
brotli_comp_level 6;
brotli_static on;
brotli_types text/plain text/css application/javascript application/x-javascript text/xml 
application/xml application/xml+rss text/javascript image/x-icon 
image/vnd.microsoft.icon image/bmp image/svg+xml;`
Save and close the file, then verify the Nginx for any syntax errors:

```bash
nginx -t
```
You should get the following output:
`
nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful
Next, start the Nginx service using the following command:`

```bash
systemctl start nginx
```