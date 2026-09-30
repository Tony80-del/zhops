# zhops · 中文课线上排课系统

面向越南中文教学业务的排课系统。**管理端 + 教师端两个页面**，单文件零依赖，数据存在浏览器 `localStorage`（暂未上云）。

## 线上地址

| 页面 | 地址 |
|---|---|
| 管理端（排课系统） | https://tony80-del.github.io/zhops/ |
| 教师端（开班申请） | https://tony80-del.github.io/zhops/teacher.html |

## 这个仓库是什么

**只是发布产物**，不是源码仓库。不要在这里直接改代码 —— 下次发布会被覆盖。

- 源码在 `~/WorkBuddy AI/2026-09-28-16-30-19/chinese-class/docs/`
  - `schedule.html` → 管理端
  - `teacher-apply.html` → 教师端
- 发布脚本：`chinese-class/build/publish-zhops.sh`
- 本地短链：`~/schedule.html` / `~/teacher-apply.html`

## 怎么重新发布

```bash
cd ~/"WorkBuddy AI/2026-09-28-16-30-19/chinese-class"
sh build/publish-zhops.sh
```

脚本会复制实体文件到本仓库并 commit + push。**必须是复制实体文件**：GitHub Pages 不跟随软链，把 `~/schedule.html` 这种软链提交上去，线上打开只会显示一行路径文字。

## 功能概览

- 左侧一个总表单管全部设置，小节顺序：**教师 → 参数 → 学员 → 时段**
- 开班表单以教师为主，字段顺序：**① 教师 → ② 开班名称 → ③ 学员人数 → ④ 时段**，按人数从候选池自动编入
- 时段 / 教师 / 学员 / 班级 / 成员 / 申请 —— 六类实体全部可增删改
- 逻辑关联：改教师身份同步班级、改级别重新对齐进度、删实体做占用检查、导入修复悬空引用
- 结算：金额一律**越南盾 VND（₫）**，`400.000 ₫` 格式
- 数据页：导出 / 导入 JSON 备份（上云前的安全网）
- 教师端生成申请码 → 管理端导入 → 审核建班

## 待办

- [ ] 第 2 步：接 Firestore + Firebase Auth（改云端规则前先出方案）
- [ ] 第 3 步：排课数据上云，多人共用
- [ ] 教师端邀请码，防垃圾提交

## 测试

源码仓库里 `sh build/run-tests.sh` —— 9 个文件、全绿。

---

私有数据不在这个仓库里：系统数据全部存在使用者自己的浏览器，仓库只有页面本身。
