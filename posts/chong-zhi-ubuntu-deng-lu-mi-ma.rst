.. title: 重置Ubuntu登录密码
.. slug: chong-zhi-ubuntu-deng-lu-mi-ma
.. date: 2016-08-18 12:22:35 UTC+08:00
.. tags: ubuntu
.. category: OS
.. link:
.. description:
.. type: text
.. author: YONG

经常在Windows上通过VirtualBox来使用Ubuntu, 很长一段时间没有登录, 居然把用户密码忘记了(或者是升级VirtualBox后的Bug?). 只能通过Grub重置密码了. 其本参照 https://help.ubuntu.com/community/LostPassword 这里的方法, 步骤如下:

1. 启动Ubuntu时长按Shift键进入Grub菜单
2. 选择recovery mode选项回车
3. 选择"root Drop to root shell prompt"选项
4. 在 ``~#`` 符号后输入 ``mount -rw -o remount /`` 使root盘获取读写权限. 如果略过此步执行下一步可能会提示"Authentication token manipulation error"
5. 在 ``~#`` 符号后输入 ``passwd [username]`` 按提示设置新的密码
6. 输入 ``reboot`` 重启.
