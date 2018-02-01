# fail2ban 安裝與設定

```bash
# Install fail2ban
apt-get install -y fail2ban

rm -rf /etc/fail2ban/jail.local
touch /etc/fail2ban/jail.local

cat > /etc/fail2ban/jail.local <<EOF
[DEFAULT]
ignoreip = 127.0.0.1
maxretry = 3
findtime = 600
bantime = 3600

[ssh-iptables]
enabled = true
filter = sshd
action = iptables[name=SSH, port=ssh, protocol=tcp]
logpath = /var/log/auth.log
maxretry = $maxretry
findtime = $findtime
bantime = $bantime
EOF

service fail2ban restart
service ssh restart
```

ignoreip：忽略的 IP 清單

maxretry：登入失敗幾次後封鎖

findtime：在多久時間之內，單位（秒）

bantime：封鎖的時間，單位（秒）



