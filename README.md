# MPV Config
带有一些优化体验的自制脚本的 MPV 配置文件

## 使用

**以下为 Windows 使用方法**

### 安装

0. 启用 [Windows 开发人员模式](https://docs.microsoft.com/windows/apps/get-started/enable-your-device-for-development) 和 Git 符号链接支持 (`git config --global --bool core.symlinks true`)
1. 克隆存储库: `git clone --recursive https://github.com/Hill-98/mpv-config.git mpv-config`
2. 执行配置脚本: `powershell mpv-config\setup\setup.ps1`
3. 修复 git 符号链接错误: `powershell mpv-config\setup\fix-symbolic-link.ps1`
3. 打开 Windows 设置或控制面板设置文件关联。

### 更新

```
git pull
git submodule init
git submodule update
powershell setup\setup.ps1
powershell setup\fix-symbolic-link.ps1
```

## 说明

**控制界面:** [UOSC](https://github.com/tomasklaen/uosc) (有右键菜单)

**默认渲染配置 (gpu-hq-max):**
* `gpu-hq`
* `scale` = `ewa_lanczossharp`
* 去带: 关闭
* 着色器: [`KrigBilateral`](https://gist.github.com/igv/a015fc885d5c22e6891820ad89555637), [`SSimSuperRes`](https://gist.github.com/igv/2364ffa6e81540f29cb7ab4c9bc05b6b)
* 垂直同步 (`tscale=oversample`)

> 可以使用快捷键 `~` 回退到 `gpu-hq`，然后还可以使用快捷键 ``Alt+` `` 回退到 `default`。

**默认配置:**
* 特定于文件的配置文件
* 中文音频/字幕优先 (日文、英文其次)
* 退出时保存对当前文件的部分配置
* 始终启用缓存 (1G)
* 模糊匹配外部音频文件
* 自动检测 icc 配置文件
* 垂直同步
* 增强的去带参数
* 字幕字体: 文泉驿微米黑

**极速模式:** 卸载所有着色器、还原占用性能的配置文件、开启硬件解码。(适合低性能设备播放 4K60FPS 等视频文件时开启)

**默认保存的文件设置:**
```conf
af 音频过滤器
vf 视频过滤器
aid 音频轨道
sid 字幕轨道
vid 视频轨道
deband 去带
panscan 平移和扫描
pause 暂停状态
speed 播放速度
video-rotate 视频旋转
video-sync 垂直同步
video-zoom 视频缩放
sub-delay 字幕延迟
sub-font-size 字幕字体大小
sub-pos 字幕位置
```

> 可以使用快捷键 `DEL` 删除当前文件保存的设置。

**不完整快捷键列表:**
```conf
BackSpace 重置播放速度
Alt+= 增加字幕字体大小
Alt+- 减小字幕字体大小
Alt+UP   字幕位置向上
Alt+DOWN 字幕位置向下
Alt+RIGHT 字幕延迟增加
Alt+LEFT  字幕延迟减少
Shift+RIGHT 快进 60 秒
Shift+LEFT  倒退 60 秒
PAGE DOWN 播放列表上一个
PAGE UP   播放列表下一个
[ 上一帧
] 下一帧
< 减少播放速度
> 增加播放速度
A 显示字幕轨道列表
C 显示章节列表
d 切换去带
f 切换全屏
H 开启/关闭 硬件解码 (默认关闭)
m 切换静音
o 打开文件
p 显示播放进度
P 显示播放列表
r 旋转视频
R 从头开始播放视频
s 截图 (默认保存至桌面)
S 显示音频轨道列表
t 显示系统时间
v 开启/关闭 垂直同步 (默认开启)
V 显示视频轨道列表
Ctrl+c 切换自动裁剪黑边
Ctrl+p 填充黑边使视频比例与当前窗口比例相同 (解决视频比例大于屏幕比例时字幕位置偏高)
```

## 自定义配置

**为了方便自定义配置，我编写了一些辅助脚本，既可以自定义配置，又不会覆盖原有的配置文件，方便后续更新。**

如果你需要自定义或覆盖默认设置，可以修改配置目录的 `local.conf` 文件。

如果你需要修改默认加载的预设配置文件 (profile)，可以在配置文件目录创建 `profiles.local`，语法可以参考 `profiles` 文件。

如果你需要自定义快捷键，并且需要继承原有快捷键配置，可以按以下步骤进行操作:
1. 在 `local.conf` 文件加入已下行:
```
input-conf="~~/.input.conf"
script-opts-append="custom-input-enable=yes"
```
2. 在配置目录创建 `input.local.conf` 文件并加入以下行:
```
#@ ~~/input.conf
```
3. 在 `input.local.conf` 文件设置新的快捷键
4. 每次更改文件后，启动 mpv 并退出，新的快捷键将在下次启动时生效。

## 特色功能

### Auto Press Key

### WebPlay
