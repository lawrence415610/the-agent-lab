# 从零开始自学Agent智能体
通过提问和一系列小实验来学习Agent

## Day 1
1. 什么是Agent？Agent和LLM有什么不同？
> Agents are systems that independently accomplish tasks on your behalf. A workflow is a sequence of steps that must be executed to meet the user’s goal. Applications that integrate LLMs but don’t use them to control workflow execution—think simple chatbots, single-turn LLMs, or sentiment classifiers—are not agents. <a href="https://openai.com/business/guides-and-resources/a-practical-guide-to-building-ai-agents/">Openai</a>

Agent是能够独立解决问题的系统。它能够把一个目标拆解成多个步骤形成工作流（workflow），保留相关语境和记忆（memory），调用工具（tool），并且能够可靠地、独立地解决问题。LLM大语言模型，比如chatbot，是根据一个用户的输入来对应产生一个输出。

Agent通过LLM来管理workflow的执行，此外Agent可以动态地根据工作流当前的状态来选择工具（tool）。

简单粗暴地说，现在的Agent就是通过把LLM组织起来来完成工作流。

比如要去完成订飞机票这样的目标需要对比全网价格，找到合适的时间，然后填写订票人的信息，付款，最终完成订票。这一些步骤会形成一个工作流。

而Agent智能体就是能够稳定帮你实现这样一个工作流的东西。软件实现了自动化，我们把很多流程变成了产品APP里面的界面和步骤，但我们依然需要在关键的地方填写表格，做个人偏好的决定等等。智能体就是根据我们给它的上下文和记忆，替代我们独立去完成这个事的代理。

2. Agent可以帮助我们实现什么样的需求？
Agent可以帮助我们实现的需求往往具有三大特点：
a. 需要做复杂的决定 - 大量需要判断，处理异常，理解上下文语境的决定。
b. 难维护的规则 - 规则太多导致的更新会造成大量错误
c. 大量的不规则的数据 - 比如从用户对话中获取信息
这些需求是在传统的自动化程序工具的基础上为

3. 什么是MCP？
> Model Context Protocol (MCP) is an open-source standard created by Anthropic that allows AI models (like Claude or ChatGPT) to securely connect to external data sources, applications, and tools.

MCP是一个开源协议，它诞生的主要目的就是让LLM以标准的方式去调用工具和数据，这样一来就像大脑连上了手。这里有一个简单伪·MCP实现：要求LLM输出一个json格式的数据，再用python来根据这个json调用工具：

```json
{
  "tool": "create_markdown_file",
  "arguments": {
    "filename": "mcp实验.md",
    "content": "这就是mcp的原理"
  }
}
```

```python
import json
from pathlib import Path


def create_markdown_file(filename: str, content: str) -> None:
    path = Path(filename)
    path.write_text(content, encoding="utf-8")
    print(f"Created file: {path.resolve()}")


def main() -> None:
    with open("action.json", "r", encoding="utf-8") as f:
        action = json.load(f)

    if action.get("tool") != "create_markdown_file":
        raise ValueError("Unsupported tool")

    args = action.get("arguments", {})
    create_markdown_file(
        filename=args["filename"],
        content=args["content"]
    )


if __name__ == "__main__":
    main()
```

其实就这么简单，LLM负责输出一个json，然后用脚本根据这个json去实现功能。
如此一来LLM具备了调用工具的能力。