# deebot-client
Crate deps for gentoo
## how to upgrade x.y.z version to new version a.b.c
### Create a temp ebuild
Copy last x.y.z version deepbot-client ebuild in new version 
```bash
cd /var/db/repos/xxx/dev-python/deebot-client
```
```bash
cp deebot-client-x.y.z.ebuild deebot-client-a.b.c.ebuild
```
comment part for crates tarball in SRC_URI : 
```bash
SRC_URI="
    https://github.com/DeebotUniverse/client.py/archive/refs/tags/${PV}.tar.gz -> ${P}.tar.gz"
#   https://github.com/xavierforestier/deebot-client/releases/download/v${PV}/deebot_client-v${PV}-crates.tar.xz"
```


unpack src
```bash
ebuild deebot-client-12.0.0.ebuild digest clean unpack
```
### Generate crates tarball
```bash
pushd /var/tmp/portage/dev-python/deebot-client-a.b.c/work/deebot_client-a.b.c
```
```bash
pycargoebuild --crate-tarball -f
```
```bash
mv /var/cache/distfiles/deebot_client-0.0.0-crates.tar.xz /tmp/deebot_client-va.b.c-crates.tar.xz
```
Upload tarball /tmp/deebot_client-va.b.c-crates.tar.xz in github as a new release / tag 

### Final ebuild

Edit ebuild and uncomment cartes tarball part
```bash
popd 
```
```bash
ebuild deebot-client-a.b.c.ebuild digest clean
```
