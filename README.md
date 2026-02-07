# Telebutton

Telegram 交互式按钮 Skill for OpenClaw - 可配置的内联键盘菜单库

## 简介

Telebutton 是一个用于在 Telegram 中创建交互式按钮菜单的 Python 库。它提供简单的 API 来展示选择按钮并获取用户反馈，支持多级嵌套菜单。

## 特性

- ✅ **配置驱动** - 通过 YAML/JSON 定义按钮结构
- ✅ **多级嵌套** - 支持无限层级子菜单
- ✅ **临时状态** - 无需数据库，开箱即用
- ✅ **通用接口** - 与执行逻辑解耦

## 快速开始

### 基础用法

```python
from telebutton import ButtonMenu, show_menu, wait_selection

menu = ButtonMenu(
    question="选择执行方式：",
    options=[
        {"text": "本地运行", "callback": "local"},
        {"text": "远程服务器", "callback": "remote", "sub_menu": {
            "question": "选择服务器：",
            "options": [
                {"text": "HPC-01", "callback": "hpc_01"},
                {"text": "HPC-02", "callback": "hpc_02"}
            ]
        }}
    ]
)

show_menu(menu)
result = wait_selection()
print(f"用户选择了: {result['callback']}")
```

### 确认对话框

```python
from telebutton import show_confirm

result = show_confirm("确定要删除吗？")
if result['callback'] == 'yes':
    delete_file()
```

## 文档

- [SKILL.md](SKILL.md) - 完整使用指南
- [references/examples.md](references/examples.md) - 7个示例 + 5个Bad Cases
- [references/api.md](references/api.md) - API 参考文档

## Bad Cases 总结

1. ❌ 该用按钮时用文本列举
2. ❌ 一行放太多按钮
3. ❌ 回调标识冲突
4. ❌ 按钮缺少详细说明
5. ❌ 使用文本数字菜单而不是内联按钮

## 安装

```bash
# 克隆仓库
git clone https://github.com/liush2yuxjtu/telebutton.git

# 使用
from telebutton import ButtonMenu, show_menu, wait_selection
```

## 依赖

- Python >= 3.8
- PyYAML (可选，用于 YAML 配置)

## 许可证

MIT License

## 作者

- GitHub: [@liush2yuxjtu](https://github.com/liush2yuxjtu)

---

**核心原则**: 永远优先使用内联按钮（InlineKeyboardButton）
