# crack-elasticsearch-by-docker

Crack elasticsearch 6.x by docker

适用于破解 elasticsearch 6.x 的自动脚本

参考[wolfbolin/crack-elasticsearch-by-docker](https://github.com/wolfbolin/crack-elasticsearch-by-docker/)进行了少量修改，使用镜像自带的Python2进行文本替换，需要7.x/8.x版本的可以使用原项目

已测试版本

- elasticsearch 6.8.2

## Usage

Get srcipt

获取脚本源码

```shell
git clone https://github.com/wolfbolin/crack-elasticsearch-by-docker.git
```

Run srcipt with version

运行脚本并指定完整版本（例如: 6.8.2)

```shell
cd crack-elasticsearch-by-docker
version=6.8.2
bash crack.sh $version
```

Get cracked x-pack-core-$version.jar

编译产物和编译中间件保存在 output 文件夹中

```shell
cp output/x-pack-core-$version.crack.jar x-pack-core-$version.jar
```

## Others

You can change `crack.sh` shell with http_proxy / https_proxy url

你可以修改`crack.sh`以使用代理访问网络，避免网络访问故障

```shell
docker build --no-cache -f Dockerfile \
  --build-arg VERSION="${version}" \
  --build-arg HTTP_PROXY="http://1.2.3.4:8080" \
  --build-arg HTTPS_PROXY="http://1.2.3.4:8080" \
  --tag ${service_name}:${version} .

docker run -it --rm \
  -v $(pwd)/output:/crack/output \
  -e HTTP_PROXY="http://1.2.3.4:8080" \
  -e HTTPS_PROXY="http://1.2.3.4:8080" \
  ${service_name}:${version}
```
