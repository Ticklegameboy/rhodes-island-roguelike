# 罗德岛 · 舰内档案

[在线试玩](https://ticklegameboy.github.io/rhodes-island-roguelike/)

明日方舟同人肉鸽网页游戏：18 名干员、横版罗德岛基地、古堡三章九关与成长构筑。
WASD / 方向键移动，空格闪避，伙伴自动攻击；成长卡整卡单击领取。
当前没有跨刷新存档，刷新会重置本局。

## 仓库与部署

仓库公开可读；只有仓库所有者及其明确授权的协作者可以写入。外部访问者不能直接修改本仓库。

首次通过 GitHub 网页上传，完整源码与原始素材保存在 17 个小于 10 MB 的分包中；GitHub Actions 校验 SHA-256 后在构建目录展开，再构建、测试并发布到 GitHub Pages。工作流对源码只有读取权限，不会写回仓库。

下载全部文件后，在仓库根目录运行以下命令还原源码（需要 Node.js 与 tar）：

```bash
node --input-type=module -e "import fs from 'node:fs';import crypto from 'node:crypto';const m=JSON.parse(fs.readFileSync('game-source-manifest.json'));const b=Buffer.concat(m.parts.map(p=>fs.readFileSync(p)));if(crypto.createHash('sha256').update(b).digest('hex')!==m.archiveSha256)throw Error('Integrity mismatch');fs.writeFileSync('game-source.tar.gz',b)"
tar -xzf game-source.tar.gz
npm ci
npm run build
npm test
npm run dev
```

本地直接修改源码后，发布前需要更新完整分包和清单，或将展开后的源码提交并移除分包/清单；仅修改仓库根目录的源码文件，不能覆盖旧分包中的同名文件。

原作名称、角色及美术相关权利属于各自权利人；本项目为非官方同人作品。来源记录随源码保存在 docs 与素材元数据中。
