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




