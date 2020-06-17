# fedora workstation

## 开启 sshd

fedora workstation 默认未开启 sshd 服务，若想远程登录到该机器，需要启用 sshd：

```
sudo systemctl enable sshd
sudo systemctl start sshd
```