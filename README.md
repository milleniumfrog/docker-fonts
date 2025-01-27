# docker-fonts

This container build a static nginx webserver with font files.

To get rid of all build dependencies, we use multi-stage build. 

Nevertheless the finished image has a size of about >4GB due to the font files.

To see which fonts are available, the directory index for the font directories is activated in the nginx config.

If you need SSL we recommend to use a proxy like [jwilder/nginx-proxy](https://github.com/jwilder/nginx-proxy) in front of this container.

### Google Fonts

- src: https://github.com/google/fonts/ 
- fonts are available in /google-fonts/* directory in DocumentRoot

Since the master file only provides ttf formats, all existing fonts are also converted to woff, woff2 and eot formats.

Tools used to convert fonts:
- for woff2 https://github.com/google/woff2.git
- for woff, and eot https://github.com/ananthakumaran/webify


### ionicons

- src: https://github.com/driftyco/ionicons/archive/v2.0.1.zip
- fonts and CSS files are available in /ionicons/* directory in DocumentRoot


## glyphicons 
- src: https://github.com/twbs/bootstrap/tree/v3.3.7/fonts
- glyphicons fonts v1.9, bundled within bootstrap 3 were released under the same license MIT License as Bootstrap. 
- Newer versions are no longer available under a free license, see: https://glyphicons.com/old/license.html#old-halflings-bootstrap and https://github.com/twbs/bootstrap/issues/3942#issuecomment-504103949

## build

Since converting the individual fonts (especially for woff2) takes time, building can take quite a long time.

    docker build . -t docker-nginx-fonts

## run

    docker run --rm -p1080:80 -d --name fonts-server docker-nginx-fonts
   
## run bash inside container

    docker exec -it fonts-server bash
