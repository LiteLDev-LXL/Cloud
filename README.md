# UpService V2
欢迎，这里是LXL开源项目的公共更新检查服务，旨在为开发者减少花费在检查更新上的时间与金钱。相比自建更新检查，本项目：
 - 完全免费
 - 稳定，JSD全球高速连接

另外，相对于单纯使用Jsdelivr的更新检查，本项目：
 - 使用随机目录名绕过缓存，JSD在大陆的缓存很难使用Purge刷新。
 - 支持自动对文件生成MD5校验文件
 - 支持自定义自动运行脚本

## TOS
 - **不要修改 `id.json` 文件**
 - **不要修改随机文件夹的文件夹名**
 - 不要修改随机文件夹中的文件，这是无效的！
 - 不要修改其他人文件夹中的文件，除非得到授意。
 - 如果使用__AUTORUN__.sh，**不要在脚本中放置任何恶意代码**
 - 如果使用__AUTORUN__.sh，**及时修改脚本中的错误(如果有)** 因为这会中断Actions进程。
 - 存储的内容不得违反Jsdelivr或Github相关政策
 > LXL Team保留对所有文件和成员操作权限的管理权力，<br>
 > 如果你对以上内容有异议，请勿使用本存储库服务。如果你违反了以上TOS，您的相关权益可能被撤销。

## Usage
 - **基础** 请在本Repo中新建一个属于自己(插件)的文件夹，您将负责维护此文件夹。
 - **基础** 获取随机文件夹名（id.json）
> 本项目使用Github Actions，每次提交都会根据提交SHA1刷新目录名。因此，相对于传统的检查更新代码，只需加一个获取这个“目录名”的步骤即可。这里提供一个示例，供参考：
```javascript
// 原代码
let server = "https://cdn.jsdelivr.net/gh/LiteLDev-LXL/Cloud/"
// 加入
let tknServ = "https://lxl-cloud.amd.rocks/id.json" // 单纯使用Jsdelivr仍然不能绕过id缓存，因此使用Cloudflare CDN下载id文件，获取id后再使用速度较快的Jsdelivr进行后续操作
let token = JSON.parse(HttpGet(tknServ).data).token + "/"
server += token
// 其余代码不变
```
 - **进阶** 运行自定义脚本
 > 此功能为方便开发者而提供，Actions将运行目录下所有`__AUTORUN__.sh`文件。
 
 本项目Actions使用Windows系统，但你需要用`bash`语法来编写脚本。<br>
 一个应用示例：
 ```bash
 # Path: ./iLand/__AUTORUN__.sh
 # iLand 自动从上游仓库同步语言文件到此仓库
 rm -rf i18n-data
 git clone https://github.com/LiteLDev-LXL/iLand-Core.git
 cp -R iLand-Core/3rd-languages/ i18n-data
 cp -R iLand-Core/iland/lang/ i18n-data
 rm -rf iLand-Core
 echo "iland's corn is completed."
 ```
  - 编写完成后，请务必关注脚本在Actions中的运行情况。如果导致Actions中断，请立即修复或删除你的脚本。

## Important
 - **如何提交至仓库** 提交到根目录即可，不要修改随机文件夹
 - **IgnoreDirs如何使用** 以根目录为基准即可，不需要计算MD5的文件夹名每行一个
 - **切记Jsdelivr使用随机文件夹名访问** 若不使用，可能存在缓存
 - **切记获取id.json使用AMD域名** 若不使用，可能导致404（因为JSD缓存没刷新）

## Credits
 - MD5自动计算程序 [@yqs112358](https://github.com/yqs112358)
 - 一切的基础 [@jsdelivr](https://github.com/jsdelivr)
