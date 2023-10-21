## git 设置

```bash
git config --global user.name "runoob"
git config --global user.email test@runoob.com

ssh-keygen

//http || https
git config --global http.proxy 127.0.0.1:7890
git config --global https.proxy 127.0.0.1:7890

//sock5代理
git config --global http.proxy socks5 127.0.0.1:7890
git config --global http.proxy socks5 127.0.0.1:7890

// 查看代理
git config --global --get http.proxy
git config --global --get https.proxy

// 取消代理
git config --global --unset http.proxy
git config --global --unset https.proxy
```

## 设置代理

```bash
export http_proxy=http://192.168.51.81:7890 && export https_proxy=http://192.168.51.81:7890
export http_proxy=http://192.168.1.107:7890 && export https_proxy=http://192.168.1.107:7890
```

## 没有网络

```bash
sudo dhclient -v
```
