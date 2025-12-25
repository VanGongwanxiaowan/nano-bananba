https://linguista.bearblog.dev/complete-developer-tutorial-for-nano-banana-pro/?utm_source=chatgpt.com

# Nano Banana Pro 完整开发者教程总结
## 一、教程基础信息
1. **来源与定位**：翻译自Google AI Studio文章，聚焦Nano Banana Pro（Gemini 3 Pro Image）AI模型，旨在指导开发者借助Gemini开发者API，掌握其高级功能以构建复杂创意应用。
2. **核心差异**：相较于基础版Flash模型（Nano Banana），Pro版本新增“思维”能力、搜索溯源功能及高保真4K输出，更适用于复杂创意任务，但无免费层级，需付费使用。
3. **配套资源**：提供交互式版本，包括Python指南（Cookbook）和AI Studio的Javascript笔记本，方便开发者实操。

## 二、前期准备（项目设置）
### 1. 必备条件
- **API密钥**：登录Google AI Studio后，系统自动创建Google Cloud项目及API密钥，可在API密钥管理屏幕复制。
- **计费启用**：因Pro版本无免费额度，需在API密钥管理屏幕点击“设置计费（Set up billing）”，按提示完成配置。
- **SDK安装**：支持Python与JavaScript/TypeScript语言，对应安装命令如下：
  - Python：`pip install -U google-genai`、`pip install Pillow`（图像处理库）
  - JavaScript/TypeScript：`npm install @google/genai`

### 2. 费用说明
- 生成1K或2K图像费用为$0.134，4K图像为$0.24（另加输入和文本输出的token费用），具体以官方定价页面为准。
- 可通过批处理（Batch）API节省50%成本，但需等待最长24小时获取图像。

## 三、核心操作步骤
### 1. 客户端初始化
需使用`gemini-3-pro-image-preview`模型ID，Python示例代码如下：
```
from google import genai
from google.genai import types
# 初始化客户端
client = genai.Client(api_key="YOUR_API_KEY")
# 设置模型 ID
PRO_MODEL_ID = "gemini-3-pro-image-preview"
```

### 2. 基础生成（经典用法）
通过`response_modalities`（控制输出文本+图像或仅图像）和`aspect_ratio`（设置宽高比，可选“1:1”“2:3”等多种比例）控制输出，示例为生成特定眼部颜色的暹罗猫图片。

### 3. 关键高级功能
|功能|说明|操作要点|
|----|----|----|
|“思维”过程|生成图像前对提示词推理，且可查看推理过程|在`thinking_config`中设置`include_thoughts=True`，输出时可获取“思维”文本与图像|
|搜索溯源|访问Google搜索实时数据生成准确图像|配置`tools=[{"google_search": {}}]`，需展示图像来源，示例为生成东京5天天气预报图|
|4K生成|支持打印级4K分辨率输出|在`image_config`中设置`image_size="4K"`（分辨率选项需大写，另有“1K”“2K”），注意成本较高|
|多语言能力|生成并翻译图像中的文本，支持十几种语言|先生成指定语言图像（如西班牙语广义相对论信息图），再发送翻译指令（如译为日语）|
|高级图像混合|最多可混合14张图像，适合复杂拼贴或产品线展示|在`contents`中传入提示词与多张图像（如办公室人员鬼脸合影），追求高保真度建议限制在5张以内|

## 四、Pro专属功能演示
1. **个性化像素艺术**：结合搜索溯源，查找人物（如Guillaume Vernade）具体信息，生成等轴测视角的详细像素艺术以展示其职业生涯。
2. **复杂文本集成**：生成含特定内容的信息图，如包含香蕉主题十四行诗及详细文学分析、复古风格的十四行诗原理信息图，可完美集成连贯长文本。
3. **高保真样机**：创建逼真印刷品样机，例如精致剧院座位上、关于TCG玩家的百老汇演出节目单照片，呈现准确光照与纹理。

## 五、最佳实践与提示词技巧
1. **极度具体**：明确主体、颜色、光照、构图等细节，增强对输出的控制权。
2. **提供上下文**：说明图像目的或期望氛围，辅助模型做出合适创意选择。
3. **迭代优化**：利用对话能力逐步调整，优化图像效果，不追求一次成型。
4. **分步指令**：复杂场景下，将提示词拆分为清晰、连续的步骤。
5. **正面描述**：避免“没有汽车”等负面表述，改用“空旷、废弃且无交通迹象的街道”等正面描述。
6. **善用搜索溯源**：需实时/现实数据时明确指令，如“搜索奥林匹克里昂队上一场比赛信息并制作图表”。
7. **降低成本**：通过批处理API批量发送请求，节省50%成本且获取更高配额，需接受最长24小时等待。

## 六、参考与后续操作
1. 深入学习：查阅官方提示词指南及Nano Banana提示词最佳实践博客。
2. 实操入口：前往Google AI Studio，尝试或自定义应用，或查看指南（cookbook）。
3. 相关链接：包含Google AI Studio、Gemini开发者API、定价页面、批处理API等官方链接，以及Python指南、Javascript笔记本等配套资源链接。
