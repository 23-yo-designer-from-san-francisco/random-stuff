Bind folders with different owner
```bash
sudo bindfs -u www-data -g www-data /root/tracks /root/2021_2_LostPointer_front/src/static/tracks
bindfs -u www-data -g www-data /root/tracks /root/2021_2_LostPointer_front/src/static/tracks
bindfs -u www-data -g www-data /root/2021_2_LostPointer_front /usr/share/nginx/front
```
