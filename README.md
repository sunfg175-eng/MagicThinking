# Gemini 字幕生成软件相关思考
## 需求提出
  **Q**：一款音频生成字幕文件的应用，以下是我的需求 音频提交上传，生成双语字幕文件，这双语包含 识别到的语言和中文， 同一时间戳下，不同语言分为两个细目，识别语言在上，中文在下。中文字幕样式使用古典体。
  **A**：
    推荐技术栈 Python Streamlit 
    推荐模型 Whisper
      
1.网站需要对外发布
 **Q** 基于Whisper对CPU/GPU的消耗，多人上传的并发问题，pytorch库部署体积过大
 **A**：
    whisper换成OpenAI whisper-1 API

2.希望开发费用低
   **Q**Api 国内获取复杂且需要付费
   **A**：
    使用Cloudflare，有免费的Workers AI调用。
    前端python Stramlit 云托管
    后端cloudflare worker ai（REST API 调用）
          语音识别: @cf/openai/whisper
          翻译: @cf/meta/llama-3-8b-instruct (用大模型翻译更精准) 或保留 deep-translator。deep-                translator。这是一个 Python 库，它利用了 Google Translate 等服务的免费接口（不需要 Key，虽有           一定频率限制，但对个人小项目足够）

3.扩展应用
  **Q** 当前提供方案单次音频处理 Max 15MB，目前有一个长达三小时的音频需求。
  **A** 
    音频切割 FFmpeg
    翻译 deep-translator 相对稳定

4.实时股票检测软件
数据来源
https://www.joinquant.com/
https://tushare.pro/register
AKShare


