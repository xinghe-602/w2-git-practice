# w2-git-practice · 可复现 Python 环境最小实验

从空目录建一个可复现的隔离环境的小实验。

## 为什么需要它

为了给每个项目提供干净、独立的 Python 运行环境，避免相互之间互相干扰。

## 环境要求

- Python 3.12+
- 依赖见 `requirements.txt`

## 复现步骤
Windows 下 cmd/PowerShell 与 Git Bash **二选一**执行即可，激活成功的标志是命令行前出现 `(venv)`。
**cmd/powershell**
```bash
python -m venv venv
.\venv\Scripts\activate 
pip install -r requirements.txt
python test.py  
```

**git bash(MINGW64) —— \会被当成转义符吃掉，必须写成/d/开头**
```bash
python -m venv venv
source venv/Scripts/activate
pip install -r requirements.txt
python test.py
```

看到绿色输出 `venv + rich 跑通了！`，说明环境已经原样复活。

## 踩过的坑
**Git Bash 不认 Windows 反斜杠** —— `cd D:\个人提升\w2-venv-lab` 报 No such file or directory，因为 `\` 被当成转义符吃掉，要写成 `cd /d/个人提升/w2-venv-lab`。

**.gitignore 规则名和实际目录名必须完全一致** —— 写 `.venv/` 而目录叫 `venv/`，整个虚拟环境被推上了 GitHub。

**git push 报 403** —— 用了登录密码或 fine-grained token（默认无 push 写权限），必须用 Classic PAT 且勾 repo。

## 文件说明

| 文件 | 说明 |
|---|---|
| `.gitignore` | 不提交虚拟环境、`__pycache__`、`.idea` 的规则文件 |
| `requirements.txt` | `pip freeze` 导出的依赖清单，用 `pip install -r` 装回 |
| `test.py` | 验证脚本，能打印即环境成功 |
| `demo.txt` | 练 git add / commit 用的小文件 |


