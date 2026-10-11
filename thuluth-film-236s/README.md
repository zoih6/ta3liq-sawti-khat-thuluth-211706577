# سلطان الحرف - خط الثلث - 236 ثانية - Cinematic Paper Collage

فيلم وثائقي تحقيقي بأسلوب Vox + كولاج ورقي سينمائي فاخر

## المواصفات
- المدة: 236 ثانية (22 مشهد × 10-26 ثانية)
- المقاس: 1920x1080 16:9 أفقي
- FPS: 30fps (قابل للترقية 60fps)
- الألوان: #171615 فحمي #E8DDC5 عاجي #5A4634 بني #B89A58 ذهبي #F7F0E3 أبيض دافئ
- التعليق: تعليقصوتيخطالثلث_211706577.mp3 (236.01s)
- BPM: 123.04

## الملفات
- `index.html` - الفيلم كبرنامج: window.seek(t) ترسم كل فريم
- `cues.json` - 35 إشارة صوتية thump/whoosh/pop/click
- `beats.json` - تحليل الإيقاع من التعليق
- `assets/` - 31 أصل A01-A31 (ورق، حبر، ذهب، قصبة، مخطوطات، هندسة، بورتريهات، قبة، أختام، 9 أنواع ثلث، سكانر، فيكتور، آيباد، ليزر، خاتمة)
  - 20 عبر AI image generation
  - 11 عبر procedural PIL
- `out/` - المخرجات
  - `silent_full.mp4` - 236s صامت 1.8M
  - `sfx.wav` - مؤثرات مركبة 22M
  - `final.mp4` - نهائي مع تعليق + SFX 3.9M
  - `final_voiceonly.mp4` - نهائي مع تعليق فقط 5.6M
  - `contact.png` - كونتاكت شيت 1fps tile 6x5
  - `poster.png` - بوستر آخر فريم
- `docs/` - shotlist + style guide + asset list

## التشغيل
```bash
npm i
npm i -D playwright canvas
npx playwright install chromium
pip install numpy librosa soundfile pillow

# حلل الصوت
python scripts/beats.py assets/voiceover.mp3 > beats.json

# ولد SFX
node scripts/sfx.mjs cues.json out/sfx.wav

# رندر 4 أجزاء متوازية (أسرع)
node scripts/render_chunk.mjs --start 0 --dur 60 --fps 30 --out out/chunk_0.mp4 &
node scripts/render_chunk.mjs --start 60 --dur 60 --fps 30 --out out/chunk_60.mp4 &
node scripts/render_chunk.mjs --start 120 --dur 60 --fps 30 --out out/chunk_120.mp4 &
node scripts/render_chunk.mjs --start 180 --dur 56 --fps 30 --out out/chunk_180.mp4 &
wait

# ادمج
ffmpeg -f concat -safe 0 -i out/concat_list.txt -c copy out/silent_full.mp4

# كونتاكت شيت
ffmpeg -i out/silent_full.mp4 -vf "fps=1,scale=320:-1,tile=6x5" -frames:v 1 out/contact.png
ffmpeg -i out/silent_full.mp4 -ss 235 -vframes 1 out/poster.png

# مكس نهائي
ffmpeg -i out/silent_full.mp4 -i out/sfx.wav -i assets/voiceover.mp3 -filter_complex "[1:a]loudnorm=I=-20:TP=-1.5[s];[2:a]loudnorm=I=-14:TP=-1.5[v];[s][v]amix=inputs=2:duration=longest[a]" -map 0:v -map "[a]" -c:v copy -c:a aac -shortest out/final.mp4
```

## الأسلوب
وثائقي تاريخي تحقيقي، كولاج ورقي سينمائي، مخطوطات عربية قديمة، قصاصات ممزقة، حبر أسود، ذهب عتيق، موشن تحريري واقعي فاخر ومهيب.

## القواعد
- دالة صافية في الزمن: لا Math.random، لا timers، لا CSS transitions في وضع الرندر
- ممنوع: عنوان في المنتصف على تدرج، كل شيء يتلاشى، ملصقات زوايا، إطارات، وهج
- شيء جديد كل 2-4 ثواني، Hook أول 2 ثانية
- نص عربي: direction rtl + خط عربي

تم البناء عبر AI Film Studio v3.2.0 + MOTION-REEL-SKILL
