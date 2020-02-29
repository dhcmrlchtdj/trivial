# ssh notify

https://askubuntu.com/questions/179889/how-do-i-set-up-an-email-alert-when-a-ssh-login-is-successful/448602#448602
https://medium.com/@alessandrocuda/ssh-login-alerts-with-sendmail-and-pam-3ef53aca1381
https://blog.502.li/linux-login-alarm-telegram.html

看了 blog，感觉 telegram 监控 ssh 的想法不错

---

- 在 `/etc/ssh/sshd_config` 开启 `UsePAM yes`
- 创建 `login-notify.sh`
- 在 `/etc/pam.d/sshd` 添加 `session optional pam_exec.so seteuid log=/path/to/login-notify.log /path/to/login-notify.sh`
- 完

---

```bash
$ man 8 pam_exec
$ cat login-notify.sh

#!/bin/bash

BOT_TOKEN=''
CHAT_ID=''

text="<pre>from sshd:
ip     = ${PAM_RHOST}
user   = ${PAM_USER}
type   = ${PAM_TYPE}
date   = $(date -u +'%Y-%m-%d %H:%M:%S')
server = $(uname -nr)
</pre>"

json="{
    \"parse_mode\": \"HTML\",
    \"chat_id\": ${CHAT_ID},
    \"text\": \"${text}\"
}"

curl "https://api.telegram.org/bot${BOT_TOKEN}/sendMessage" \
    -H 'Content-Type: application/json' \
    --data "${json}"
```

