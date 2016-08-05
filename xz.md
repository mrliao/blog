大家也在经常工作中会遇到tar.xz文件，可能有的人知道怎么打包的，可能有的人知道怎么解包的，下面应该满足大多数人的需求

### `创建tar.xz文件：只要先 tar cvf xxx.tar xxx/ 这样创建xxx.tar文件先，然后使用 xz -z xxx.tar 来将 xxx.tar压缩成为 xxx.tar.xz`
### `解压tar.xz文件：先 xz -d xxx.tar.xz 将 xxx.tar.xz解压成 xxx.tar 然后，再用 tar xvf xxx.tar来解包。`
