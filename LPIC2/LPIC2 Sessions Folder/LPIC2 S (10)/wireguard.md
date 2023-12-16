---
tags:
  - LPIC
  - linux
  - command
  - concept
up: "[[LPIC 2 (session 10)]]"
date: 2023-11-15
---
### تنظیم سرور کلاینت لینوکس

```bash
apt update && apt install wireguard resolvconf
```
پکیج resolvconf مورد نیاز است.

دایرکتوری مربوط به وایرگارد رو می سازیم
```bash
mkdir /etc/wireguard
```

کلید خصوصی و عمومی را ایجاد میکنیم و در پوشه وایرگارد قرار میدهیم
دسترسی این فایل را به کاربر روت محدود میکنیم
```bash
root@vm1835730:/etc/wireguard# wg genkey > private
root@vm1835730:/etc/wireguard# wg pubkey < private
root@vm1835730:/etc/wireguard# chmod 600 private
```

برای بررسی فعال بودن وایرگارد روی کرنل ازین دستور استفاده میکنیم
```bash
root@vm1835730:/etc/wireguard# lsmod | grep wireguard
```

کارت شبکه با حالت وایرگارد ایجاد میکنیم
با دستور ip a فعال شدن کارت شبکه را بررسی میکنیم
سپس ip هر طرف تونل را در یک رنج اضافه میکنیم مثلا 10.0.0.1 و 10.0.0.2
```bash
root@vm1835730:/etc/wireguard# ip link add wg0 type wirguard
root@vm1835730:/etc/wireguard# ip a
root@vm1835730:/etc/wireguard# ip addr add 10.0.0.1/24 dev wg0
```

کلید پرایویت اینترفیس مربوطه را به آن ست میکنیم
با دستور set up اینترفیس مربوطه را up میکنیم
دستور wg اینترفیس های موجود را نشان میدهد. 
بعد از up کردن اینترفیس وایرگارد به یک پورت لیسن رندوم میکند
```bash
root@vm1835730:/etc/wireguard# wg set wg0 private-key /etc/wireguard/private
root@vm1835730:/etc/wireguard# ip link set up dev wg0
root@vm1835730:/etc/wireguard# wg
interface: wg0
  public key: Ld/cee9QS/V6NpGLEUx7CBsiu5oSEFapd60ODpsc3Ss=
  private key: (hidden)
  listening port: 42716
```

با دستور نت استت میتوانیم فعال بودن وایرگارد را چک کنیم
وایرگارد روی udp فعال است.
```bash
root@vm1835730:/etc/wireguard# netstat -lnpu
```