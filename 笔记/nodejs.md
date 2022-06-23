# node.js常用命令

```bash
# 下载包命令
npm install 包名@指定版本
npm i 包名@指定版本

# 查看下载的包
npm ls
npm list

# 生成package.json文件
npm init -y

# 一次性安装package.json中所有依赖包
npm install
npm i

# 卸载包
npm uninstall 包名

# 安装指定的包，并记录到devDependencies节点中
npm i 包名 -D
npm install 包名 --save-dev

# 查看当前的下包镜源
npm config get registry
# 切换下包镜源为淘宝镜源
npm config set registry=https://registry.npm.taobao.org/

# 卸载全局包
npm uninstall 包名 -g

# 通过npm将nrm安装为全局可用的工具
npm i nrm -g
# 查看所有可用的镜像源
nrm ls
# 将镜像源切换为淘宝镜像
nrm use taobao

# 将i5ting_toc安装为全局包
npm i i5ting_toc -g
# 调用i5ting_toc，实现md转html（用默认浏览器打开）
i5ting_toc -f md文件路径 -o

# 发布包
npm publish

# 删除包
-- 只能删除72小时以内发表的包
-- 删除的包在24小时内不能重新发布
npm unpublish 包名 --force

# 安装express
npm i express
```

