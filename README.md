# openai_api_zh
OpenAI API中文版，原始英文版请参考：https://platform.openai.com/docs/introduction/overview
> 译者注：chatGPT的诞生，译者认为是一项划时代的创新。基于OpenAI API可以构建出很多有趣的应用，为了方便英文基础不是很好的同学，我尝试翻译OpenAI API的中文版。初次翻译，很多东西译者理解也不是很深刻，因此难免有很多错误，还请读者谅解、海涵。我会不断优化该翻译，并及时将已经完成翻译的章节放到这里。
# 开始
## 简介
### 概览
OpenAI的API可被用于任何涉及自然语言理解和生成的任务。我们提供一系列不同功能等级的模型以适配您各种场景，甚至于提供模型微调（fine-tune）的能力以让您可以充分定制您的模型。
这些模型可被用于从内容理解到语义搜索及分类的任何任务。
### 关键概念
我们建议您完成我们的快速入门教程，以通过实际操作的交互式示例来熟悉关键概念。
链接到“快速开始”
1. Prompts and completions
2. Tokens   
我们的模型通过把文本拆成一个个的token来进行理解。一个Token可以是一个完整的单词，也可以仅仅是一个字符序列。举例而言，对于单词hamburger，
可能被拆分为ham、bur、ger三个token，然而一个很常见的短单词pear可能就被当做一个完整的token来处理。很多token以空格开始，比如" hello"、" bye"。   
每个API请求能处理的token数是有限制的（对于大多数模型而言，这个限制是2048个token，差不多相当于1500个英文单词），而这个tokens取决于您的问题输入和结果输出的token数的总和。作为一个粗略的估算，对于英文文本而言，一个token近似平均含有4个字符，差不多相当于0.75个英文单词长度。您可以通过tokenizer tool来了解更多关于文本是如何转换为token的知识。


3. 模型（Models）   
OpenAI的API背后是由多个不同能力和价格的模型在支撑。我们的基础模型GPT-3包括Davinci, Curie, Babbage和Ada.
我们的Codex系列模型则是在GPT-3的基础上演进过来，用于自然语言和代码的训练。
如果想了解更多，请参考  model
### 下一步指引
- 当您开始基于openAI的API构建应用时，请您记住使用限制；
- 可以从我们的案例库中找寻更多灵感
- 可以选择下列的指引开始构建您的应用
1. 文本生成
2. 代码生成
3. 图片生成
4. 模型微调
5. Embedding生成
## 快速开始
OpenAI训练了多个擅长文本理解与生成的前言语言模型。OpenAI API则是提供了用于访问这些模型从而解决各类语言处理的任务。   
在这篇快速指引里，你将基于OpenAI API构建一个demo应用。同时，你将学到一系列关于使用OpenAI API构建应用的关键概念和技术，包括：
- 内容生成
- 总结
- 分类、情感分析
- 数据提取
- 翻译
- 其他
### 简介
completions endpoin（这个词笔者实在找不到合适的反应，只好照搬了）是OpenAI API的核心，它为用户提供了一个简单、灵活且强大的交互界面。你输入一些提示性（prompt）的文本，OpenAI API将返回一个回答（称为一个completion）用于匹配你的任何输入。
Prompt：Write a tagline for an ice cream shop.    
Completion: We serve up smiles with every scoop!
你可以把这当做是一个非常先进的自动补全——背后的模型将处理你输入的文本提示，然后预测出最匹配这个提示的答案。
1. 通过一个指令开始  
假设你想创建一个给宠物起名字的应用。从一堆杂乱的字典里构造一个合适的名字是一件困难的事情。  
首先，你需要提供一个能够清楚表达你所想的描述。让我们用一个指令来开始。通过给出一个提示来得到你的第一个回答。
Prompt：Suggest one name for a horse.
Completion：How about the name "Thunderbolt"?     
看上去似乎还不错！现在我们尝试让指令更加具体：
Prompt：Suggest one name for a black horse.  
Completion：Midnight Shadow.  
如你所见，在输入的提示里添加一个形容词，就改变了返回的结果。设计输入提示的本质是你准备怎么“操作”背后的模型。  
2. 添加一下示例  
制作好的指令对于获得好的结果非常重要，但有时候也还不够。让我们尝试把上面的指令更丰富一点吧。
Prompt：Suggest three names for a horse that is a superhero.  
Completion：1. Thunderhoof   2. Gallop Guardian   3. Mane Marvel   
这个回答好像并不是非常符合我们的需要。这些名字非常普通，看上去模型并没有注意到我们是想给一匹马起名字（而是当做普通的动物）。我们是否可以提供一些相关的建议呢？  
通常来讲，向模型告知并通过示例展示你想要的结果是很有意义的。输入提示里添加一下示例可以让你更好的与模型进行沟通。让我们尝试给输入添加一些示例吧。  
Prompt：
Suggest three names for an animal that is a superhero.
Animal: Cat
Names: Captain Sharpclaw, Agent Fluffball, The Incredible Feline
Animal: Dog
Names: Ruff the Protector, Wonder Canine, Sir Barks-a-Lot
Animal: Horse
Names: The Galloping Guardian, Mighty Mustang, Super Stallion

  Completion：      
  
非常棒！通过在输入提示里添加一些示例可以更好地帮助模型给我们提供我们想要的答案。  
3. 调整你的设置   
> 译者注：待翻译
4. 构建你的应用
- NodeJS版本
现在你已经知道怎么提供一个好的输入提示和相关设置了，那就可以开始构建这个给宠物起名的应用了。这里我们提供一些代码帮助你开始，你可以跟随下面的步骤下载相关代码，然后运行你的应用。
* 安装
如果你的环境里还没有安装Node.js，请参考https://nodejs.org/en/ 进行安装。然后clone这个git仓库到你本地：
```
git clone https://github.com/openai/openai-quickstart-node.git
```
如果你不习惯于使用git，你可以直接下载这个代码压缩包：https://github.com/openai/openai-quickstart-node/archive/refs/heads/master.zip
* 添加你的API key
基于OpenAI API构建应用，必须先获得API key。你可以通过注册账号https://platform.openai.com/signup 来获得。
> 译者注：OpenAI目前没有向中国大陆用户开放，因此无法注册。可尝试通过其他方式获取API key
* 执行你的应用
在你的项目目录下执行下面的命令用于安装依赖，然后启动你的应用执行。
```
npm install
npm run dev
```
在你的浏览器里打开 http://localhost:3000 ，你将看到这个给宠物起名的应用。
* 理解代码
> 译者注：待翻译
5. 结尾  
6. 下一步
# 详细指南
# API参考
