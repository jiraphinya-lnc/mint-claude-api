<h4 align="right">
  <strong>ไทย</strong> | 
</h4>

<div>
  <h1 align="center">mint-claude-api</h1>
  <p align="center">
    <a href="https://github.com/jtsang4/claude-to-chatgpt/releases" target="_blank">
        <img src="https://github.com/jtsang4/claude-to-chatgpt/actions/workflows/docker.yaml/badge.svg" alt="release">
    </a>
    <a href="https://github.com/jtsang4/claude-to-chatgpt/releases">
        <img alt="GitHub Repo stars" src="https://img.shields.io/github/stars/jtsang4/claude-to-chatgpt?style=flat">
    </a>
    <a href="https://github.com/jtsang4/claude-to-chatgpt/releases">
        <img alt="GitHub Repo Badge" src="https://img.shields.io/badge/anthropic-claude-orange?style=flat">
    </a>
    <a href="https://github.com/jtsang4/claude-to-chatgpt/releases">
        <img alt="GitHub Repo Language" src="https://img.shields.io/badge/langurage-js/py-brightgreen?style=flat&color=blue">
    </a>
  </p>
</div>

โปรเจ็กต์นี้จะแปลง API ของโมเดล Claude ของ Anthropic เป็นรูปแบบ OpenAI Chat API

*✨ เรียก Claude API เช่น OpenAI ChatGPT API

*💦 รองรับการตอบสนองแบบสตรีมมิ่ง

*🐻 รองรับโมเดล `claude-instant-1`, `claude-2`

* 🌩️ ปรับใช้โดย Cloudflare Workers หรือ Docker

## Getting Started

คุณสามารถดำเนินโครงการนี้โดยใช้ Cloudflare Workers or Docker:

### Deployment

#### Using Cloudflare Workers

เมื่อใช้ Cloudflare Workers คุณไม่จำเป็นต้องมีเซิร์ฟเวอร์ในการปรับใช้โปรเจ็กต์นี้

1. สร้าง Cloudflare Worker
2. วางโค้ดลงไป [`cloudflare-worker.js`]() ไปยังโปรแกรมแก้ไข "แก้ไขด่วน" ของ Cloudflare Worker
3. บันทึกและปรับใช้
4. (ไม่บังคับ) ตั้งค่าโดเมนที่กำหนดเองสำหรับ Cloudflare Worker ของคุณ

Cloudflare Workers รองรับคำขอ 100,000 คำขอต่อวัน หากคุณต้องการเรียกใช้มากกว่านั้น คุณสามารถใช้ Docker เพื่อปรับใช้ตามด้านล่างนี้

#### Using Docker

```bash
docker run -p 8000:8000 wtzeng/claude-to-chatgpt:latest
```

#### Using Docker Compose

```bash
docker-compose up
```

API จะพร้อมใช้งานที่ http://localhost:8000 จุดสิ้นสุด API: `/v1/chat/completions`
### Usage

เมื่อคุณป้อนพารามิเตอร์โมเดลเป็น `gpt-3.5-turbo` หรือ `gpt-3.5-turbo-0613` มันจะถูกแทนที่ด้วย `claude-instant-1` มิฉะนั้น `claude-2` จะถูกนำมาใช้


#### GUI

ต่อไปนี้เป็นซอฟต์แวร์ GUI ที่แนะนำซึ่งสนับสนุนโครงการนี้:

* [Bin-Huang/chatbox](https://github.com/Bin-Huang/chatbox)
* [Yidadaa/ChatGPT-Next-Web](https://github.com/Yidadaa/ChatGPT-Next-Web)

#### CLI

```bash
curl http://localhost:8000/v1/chat/completions \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $CLAUDE_API_KEY" \
  -d '{
    "model": "gpt-3.5-turbo",
    "messages": [{"role": "user", "content": "Hello!"}]
  }'
```

## Conversion Details

Claude Completion API มีจุดสิ้นสุด `/v1/complete` ซึ่งรับคำขอ JSON ต่อไปนี้:

```json
{
  "prompt": "\n\nHuman: Hello, AI.\n\nAssistant: ",
  "model": "claude-instant-1",
  "max_tokens_to_sample": 100,
  "temperature": 1,
  "stream": true
}
```


และส่งคืน JSON พร้อมตัวเลือกและการกรอกข้อมูลให้สมบูรณ์

OpenAI Chat API มีจุดสิ้นสุด `/v1/chat/completions` ที่คล้ายกันซึ่งใช้:

```json
{
  "model": "gpt-3.5-turbo",
  "messages": [
    {
      "role": "user",
      "content": "Hello, AI."
    }
  ],
  "max_tokens": 100,
  "temperature": 1,
  "stream": true
}
```


และส่งคืน JSON พร้อมสตริงการตอบกลับ

โปรเจ็กต์นี้จะแปลงระหว่าง API ทั้งสองนี้ รับการดำเนินการเสร็จสิ้นจากโมเดล Claude และจัดรูปแบบเป็นการตอบกลับ OpenAI Chat

## License

โครงการนี้ได้รับใบอนุญาตภายใต้ MIT License -  LICENSE ไฟล์สำหรับดูรายละเอียด.

**พื้นที่เก็บนี้ ฉันได้เเนวคิดนักพัฒนาชาวจีนผู้ยอดเยี่ยม** 

ฉันเพียงนำมาปรับใช้ในบางสิ่งเพื่อเข้ากับบริบทคนไทย   

บางอย่างมันละเอียดอ่อนในท้องถิ่นที่เขาอาศัยอยู่ มันต่างจากกฎชุมชนในท้องถิ่นเรา

**cloude ฉันได้เนนวคิดการใช้งาน Youtube**

[Claude AI](https://www.youtube.com/watch?v=5N5rgZbIKKc&list=TLPQMTIxMjIwMjMzmfqGfF9lXg&index=4)

บรรยายโดย ผู้ช่วยศาสตราจารย์ ดร.กิตติพงษ์ สุวรรณราช , Google Certified Trainer and 

Educator, Thailand , วิทยากรรับเชิญหน่วยงานภาครัฐ และเอกชน 

อาจารย์พิเศษเกี่ยวกับเทคโนโลยีสารสนเทศ```



<h4 align="right">
  <strong>✨เกี่ยวกับ bison@001 vertex ai</strong>
</h4>
<h4 align="right">
  <strong>ฉันกำลังฝึกโมเดล mint-thai-text-bison-z 1.01 บน gg vertex ai</strong>
</h4>
  
