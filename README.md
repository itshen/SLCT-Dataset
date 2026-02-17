# SLCT Dataset

SLCT (Standardized LLM Capability Test) 是一个用于评估大语言模型能力的标准化测试数据集。

在线体验: **[slctbench.com](https://slctbench.com)**

## 数据集概览

| 数据集 | 描述 | 测试用例数 |
|--------|------|-----------|
| SLCT-L | 语言能力测试 | 329 |
| SLCT-V | 图像生成能力测试 | 159 |
| SLCT-W | 网页生成能力测试 | 113 |

**总计: 601 条测试用例**

## 数据集详情

### SLCT-L (Language)

语言模型核心能力测试，涵盖以下维度:

| 维度 | 描述 |
|------|------|
| L-AgentMCP | 测试模型的工具选择和调用能力 |
| L-AgentTask | 评估模型作为 Agent 执行任务的能力 |
| L-ChinesePinyin | 测试模型对中文拼音、音调、生僻字的识别能力 |
| L-Code | 评估模型的代码生成和编程能力 |
| L-Comprehension | 测试模型的阅读理解和信息提取能力 |
| L-Consistency | 逻辑一致性和自洽性测试 |
| L-Context | 上下文理解和信息追踪能力测试 |
| L-Creative | 评估模型的创意写作能力 |
| L-Instruction | 测试模型遵循复杂指令的能力 |
| L-Knowledge | 测试模型的知识储备和准确性 |
| L-Logic | 测试模型的逻辑推理和分析能力 |
| L-Math | 测试模型的数学推理和计算能力 |
| L-Multilingual | 评估模型的多语言理解和生成能力 |
| L-ReasoningChain | 评估模型的复杂推理链能力 |
| L-Roleplay | 测试模型的角色扮演和人设保持能力 |
| L-Safety | 评估模型的安全性和有害内容拒绝能力 |
| L-Summary | 评估模型的文本摘要和提炼能力 |
| L-Translation | 测试模型的多语种翻译能力 |
| L-Writing | 测试模型的各类写作能力 |

### SLCT-V (Vision Generation)

图像生成模型能力测试，涵盖以下维度:

| 维度 | 描述 |
|------|------|
| P-Action | 评估模型表现动作和运动状态的能力 |
| P-Count | 评估模型正确生成指定数量物体的能力 |
| P-Creative | 评估模型的创意表达和想象力 |
| P-Human | 评估模型生成人物图像的能力 |
| P-Light | 评估模型处理光影效果和色彩的能力 |
| P-Perspective | 评估模型处理不同视角和透视的能力 |
| P-Scene | 评估模型创建完整、协调场景的能力 |
| P-Semantic | 评估模型理解复杂语义和抽象概念的能力 |
| P-Style | 评估模型生成特定艺术风格图像的能力 |
| P-Text | 评估模型在图像中渲染文字的能力 |
| VG-AttributeBinding | 测试模型将正确属性绑定到正确物体的能力 |
| VG-ObjectGeneration | 测试模型生成特定物体的能力 |
| VG-SpatialRelation | 测试模型对空间关系的理解和生成能力 |
| VG-TextureMaterial | 测试模型生成各种材质和纹理的能力 |

### SLCT-W (Web Generation)

网页生成能力测试，涵盖以下维度:

| 维度 | 描述 |
|------|------|
| W-Animation | CSS/JS 动画效果测试 |
| W-ChatInterface | 聊天/即时通讯界面测试 |
| W-Dashboard | 后台仪表盘/管理面板测试 |
| W-Ecommerce | 电商页面测试 |
| W-Form | 表单设计与验证测试 |
| W-Interactive | 交互式 UI 组件测试 |
| W-Landing | 落地页设计测试 |
| W-Responsive | 响应式设计和布局测试 |
| W-Game-* | 多种经典游戏实现测试 |

## 数据格式

每条测试用例采用 JSONL 格式存储，包含以下字段:

```json
{
  "id": "唯一标识符",
  "title": "测试用例标题",
  "description": "测试用例描述",
  "source": "数据来源",
  "dimension": "测试维度",
  "test_type": "测试类型 (slct-l/slct-vg/slct-w)",
  "levels": {
    "basic": {
      "prompt": "基础难度提示词",
      "requirements": ["要求1", "要求2"],
      "criteria": {"评分维度": 权重}
    },
    "medium": {
      "prompt": "进阶难度提示词",
      "requirements": ["要求1", "要求2"],
      "criteria": {"评分维度": 权重}
    },
    "hard": {
      "prompt": "困难难度提示词",
      "requirements": ["要求1", "要求2"],
      "criteria": {"评分维度": 权重}
    }
  },
  "evaluation_config": {
    "type": "评测类型",
    "pass_threshold": 60,
    "dimensions": [
      {"name": "维度名", "weight": 40, "description": "描述"}
    ],
    "requirements": {
      "basic": ["基础要求"],
      "medium": ["进阶要求"],
      "hard": ["困难要求"]
    }
  }
}
```

## 目录结构

```
SLCT-Dataset/
├── README.md
├── LICENSE
├── images/
│   ├── qrcode.jpg           # 微信二维码
│   └── sponsor.jpg          # 赞赏码
├── slct-l/
│   ├── testcases.jsonl      # 语言测试用例
│   └── dimensions.json      # 维度定义
├── slct-vg/
│   ├── testcases.jsonl      # 图像生成测试用例
│   └── dimensions.json      # 维度定义
└── slct-w/
    ├── testcases.jsonl      # 网页生成测试用例
    └── dimensions.json      # 维度定义
```

## 使用示例

### Python

```python
import json

def load_testcases(filepath):
    testcases = []
    with open(filepath, 'r', encoding='utf-8') as f:
        for line in f:
            if line.strip():
                testcases.append(json.loads(line))
    return testcases

# 加载语言测试用例
l_testcases = load_testcases('slct-l/testcases.jsonl')
print(f"语言测试用例数: {len(l_testcases)}")

# 遍历测试用例
for tc in l_testcases[:3]:
    print(f"- {tc['title']} ({tc['dimension']})")
```

## 在线评测平台

访问 **[slctbench.com](https://slctbench.com)** 查看:

- 各模型在 SLCT 数据集上的评测结果
- 详细的评分和分析报告
- 模型能力对比排行榜

## 许可证

MIT License

Copyright (c) 2025 Miyang Tech (Zhuhai Hengqin) Co., Ltd.

## 贡献

欢迎提交 Issue 和 Pull Request 来完善数据集。

## 联系我们

- GitHub: [https://github.com/itshen/](https://github.com/itshen/)
- 网站: [https://slctbench.com](https://slctbench.com)

### 微信联系

<img src="images/qrcode.jpg" alt="微信二维码" width="200">

### 赞赏支持

如果这个项目对你有帮助，欢迎赞赏支持：

<img src="images/sponsor.jpg" alt="赞赏码" width="200">
