# Style Guide - خط الثلث - Cinematic Paper Collage

## Colors (LOCK)
- فحمي #171615 - خلفية
- عاجي معتق #E8DDC5 - ورق أساسي
- بني داكن #5A4634 - ظلال وحدود ممزقة
- ذهبي عتيق #B89A58 - عناوين ثلث محفورة
- أبيض دافئ #F7F0E3 - نصوص ثانوية

## Materials
- ورق قطني ليفي سميك 300gsm بحواف ممزقة يدوياً
- ألياف بارزة، حبر أسود مطبعي غير لامع
- معدن ذهبي محفور ب Bevel خفيف 1px
- ظلال ورقية طبيعية drop-shadow بزاوية 45° من أعلى اليسار
- تحبيب فيلمي 4% grain
- غبار دقيق في إضاءة جانبية

## Typography
- عناوين: Cairo Black 900 حجم 120-200px
- نصوص تاريخية: Amiri / IBM Plex Sans Arabic 400
- Canvas: ctx.direction='rtl', textAlign='center' or 'right'
- خط واحد للعرض وواحد للنص فقط

## Lighting & Camera
- إضاءة جانبية دافئة من أعلى اليسار 45°
- ظلال ناعمة 20px blur
- كاميرا هادئة slow push 1.0 -> 1.08 على 10 ثواني
- Parallax بين 3 طبقات ورق بسرعات 0.3 / 0.6 / 1.0

## Motion Rules
- كشف ورقي paper-reveal + انزلاق قصاصات slide 120px بـ spring(320,30)
- اقتراب سينمائي بطيء scale 1.0 -> 1.08
- اختلاف منظور Parallax
- لا يوجد fade in عام، لا وهج، لا انتقالات جاهزة
- شيء جديد كل 2-4 ثواني، Hook أول 2 ثانية

## Banned
- ألوان نيون، وهج glow، مجسمات بلاستيكية 3D
- حروف عربية مشوهة أو مقطعة، نصوص عشوائية
- حركة عصبية، انتقالات جاهزة fade عام
- عنوان في المنتصف على تدرج، ملصقات زوايا، إطارات

## Assets Generated
31 assets A01-A31:
- 20 via AI image generation (A01-A20)
- 11 via procedural PIL (A21-A31)
- All 1920x1080, editorial documentary style

## Render Spec
- 1920x1080 16:9, 30fps (target 60fps), CRF 16, yuv420p
- Duration 236s (22 scenes x ~10.7s)
- SFX synthesized via sfx.mjs (click, pop, thump, whoosh)
- Mix: voiceover -14 LUFS + SFX -20 LUFS
