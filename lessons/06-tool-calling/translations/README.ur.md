# سبق 6: ٹول کالنگ

ٹول کالنگ ، جسے فنکشن کالنگ بھی کہا جاتا ہے ، آپ کے اے آئی ماڈل میں ان صلاحیتوں کو شامل کرکے بڑھانے سے مراد ہے جن کی اس میں پہلے کمی تھی۔ اس تصور میں آپ کے فنکشنز کی میٹا تفصیلات فراہم کرنا شامل ہے ، جس سے اے آئی ماڈل کو اس بات کا تعین کرنے کی اجازت ملتی ہے کہ یوزر پرومپٹ کی بنیاد پر کسی خاص آلے کو کب بلایا جانا چاہئے۔ خیال یہ ہے کہ اسے اپنے اصل فنکشنز کی میٹا تفصیلات فراہم کریں اور اے آئی ماڈل کو اس بات کی نشاندہی کریں کہ اس طرح کے آلے کو یوزر پرومپٹ کی بنیاد پر کب بلایا جانا چاہئے۔

اس باب میں، آپ سیکھیں گے:

- ایک آلہ کیسے بنائیں.
- اے آئی ماڈل کے ساتھ ایک آلے کو ضم کریں.
- اے آئی ماڈل سے آلے کو کال کریں۔

## سیٹ اپ

اگر آپ نے پہلے نہیں کیا ہے تو ، اپنے ڈیویلپمنٹ انوائرمنٹ کو ترتیب دیں۔ یہاں ہے کہ آپ یہ کیسے کر سکتے ہیں: [اپنے ڈیویلپمنٹ انوائرمنٹ کو ترتیب دیں](/docs/setup/README.md)۔

## متعلقہ وسائل

[![فنکشن کالنگ کے ساتھ انضمام](./assets/11-lesson-banner.png?WT.mc_id=academic-105485-koreyst)](https://aka.ms/gen-ai-lesson11-gh?WT.mc_id=academic-105485-koreyst)

_یہ ویڈیو ٹول کالنگ کی وضاحت کرتا ہے ، ایک ایسا طریقہ جو اے آئی کو آپ کے فنکشنز کو کال کرنے میں مدد کرتا ہے_

*🎥 ٹول کالنگ کے بارے میں ایک مختصر ویڈیو دیکھنے کے لئے اوپر کی تصویر پر کلک کریں*

## بیانیہ: امیلیا

> _آپ 1860 کی دہائی سے لندن میں مکینک ہیں۔ اپنے آٹومیٹن پر کام کرتے ہوئے ، آپ کو چارلس بیبیج کی طرف سے ایک خط موصول ہوا جو آپ کو لائبریری میں لے گیا ، جہاں آپ نے ٹائم ٹریول ڈیوائس اٹھائی۔ اپنے سفر کے دوران ، آپ فلورنس آۓ ، جہاں آپ لیونارڈو ڈا ونچی سے ملے۔ اب آپ ایڈا لولیس سے اس کی حویلی میں ملے ہیں ، چارلس بیبیج کے ساتھ۔ وہ ٹائم ٹریول  آلہ کی تعمیر کے عمل میں ہیں._
>
> اگر آپ شروع سے کہانی کو سمجھنا چاہتے ہیں تو [سبق 1](/lessons/01-intro-to-genai/README.md) دیکھیں۔

> [نوٹ]
>  
> اگرچہ ہم کہانی کو پڑھنے کی سفارش کرتے ہیں (یہ مزہ ہے!)، [یہاں کلک کریں](#interact-with-amelia-earhart) اگر آپ براہ راست تکنیکی مواد پرجانے کو ترجیح دیتے ہیں.

**ایڈا لولیس**: "مجھے آپ کو اپنے ایک دوست سے ملوانے کی ضرورت ہے. بہت کم لوگ ہیں جو میکانکس اور مسئلہ حل کرنے میں اس کی مہارت کا مقابلہ کرسکتے ہیں۔ تاہم، اسے ملنا مشکل ہوسکتا ہے۔ وہ ہمیشہ  گھومتی رہتی ہے:)"

**آپ**: "ہم کس کے بارے میں بات کر رہے ہیں اور میں اسے کہاں تلاش کر سکتا ہوں؟"

**ایڈا لولیس**: "کیوں، ایمیلیا ایرہارٹ، بالکل! وہ ایک پائلٹ اور مہم جو ہے، اس وقت دنیا بھر میں پرواز کر رہی ہے. یہ مکمل طور پر میری غلطی ہے کہ وہ غائب ہوگئی ہے - میں نے اسے ٹائم ٹریول آلہ دیا ، اس کا ابتدائی پروٹو ٹائپ۔ خوش قسمتی سے ، آپ کے پاس موجود آلہ دوسرے آلات کو تلاش کرسکتا ہے ، تاکہ آپ اسے تلاش کرسکیں۔ آپ کو صرف یہاں اور یہاں کلک کرنے کی ضرورت ہے، اور پھر اس نوب کو موڑنا ہے."

**آپ**: "ارے، انتظار کرو، ہمارا مشن دراصل کیا ہے؟"

**ایڈا**: "اوہ، درست! آلہ سے پوچھیں۔ اس میں تمام تفصیلات ہیں. بس امیلیا کے بارے میں پوچھیں ، اور اسے آپ کے لئے صحیح ٹول شروع کرنا چاہئے۔"

آپ کے ارد گرد کی دنیا دھندلی ہونے لگتی ہے ، اور سب کچھ سیاہ ہو جاتا ہے۔ آپ آتے ہیں اور اپنے آپ کو ہوائی جہاز کے کاک پٹ میں پاتے ہیں۔ آپ ہوا میں ہیں، اور آپ اپنے نیچے سمندر دیکھ سکتے ہیں. سامنے کوئی بیٹھا ہے۔ آپ صرف ان کی گردن کے پچھلے حصے کو دیکھ سکتے ہیں.

<div>
    <img src="./assets/amelia.jpeg" alt="Amelia piloting a plane" width="300">
</div>

**آپ**: "امیلیا، کیا یہ تم ہو؟"

**ایمیلیا ایرہارٹ**: "تم کون ہو؟ مجھے اندازہ ہے، ایڈا نے آپ کو بھیجا ہے، درست؟"

**آپ**: "ہاں، ٹھیک ہے. میں آپ کی مدد کرنے کے لئے یہاں ہوں."

**امیلیا ایرہارٹ**: "ٹھیک ہے، اچھی بات ہے کہ آپ یہاں ہیں۔ میں اترنے کے لئے جگہ تلاش کرنے کی کوشش کر رہی ہوں، اور میرے پاس ایندھن ختم ہو رہا ہے. کیا آپ میری مدد کر سکتے ہیں؟"

**آپ**: "آلہ، کیا آپ مجھے ایمیلیا کے بارے میں مزید بتا سکتے ہیں؟"

**ٹائم بیٹل**: "کالنگ ٹول: مشن ایمیلیا. ٹول شروع کیا گیا. امیلیا ایرہارٹ ایک پائلٹ اور مہم جو ہے۔ وہ اپنی ریکارڈ توڑ پروازوں اور 1937 میں اپنی گمشدگی کے لئے جانی جاتی ہے۔ اسے آخری بار بحر الکاہل کے اوپر پرواز کرتے ہوئے دیکھا گیا تھا۔ وہ اس وقت اپنے طیارے الیکٹرا میں دنیا بھر میں پرواز کر رہی ہیں۔ ان کے پاس ایندھن ختم ہو رہا ہے اور انھیں اترنے کے لیے جگہ تلاش کرنے کی ضرورت ہے۔"

**آپ**: "آلہ، کیا آپ امیلیا کو اترنے کے لئے جگہ تلاش کرنے میں میری مدد کر سکتے ہیں؟"

**ٹائم بیٹل**: "کالنگ ٹول: تلاش-لینڈنگ-اسپاٹ. ٹول شروع کیا گیا. ایمیلیا ایرہارٹ کے لئے مناسب لینڈنگ جگہ کی تلاش. براۓ مہربانی انتظار کريں. لینڈنگ کے لئے مناسب جگہ مل گئی. کوآرڈینٹس: 7.5 °N, 134.5°E.  امیلیا، میں نے آپ کے لئے ایک مناسب لینڈنگ جگہ تلاش کی ہے. براہ کرم کوآرڈینیٹس 7.5 °N, 134.5°E پر جائیں۔"

**ایمیلیا ایرہارٹ**: "شکریہ! کاش میرے آلے میں یہ خصوصیت ہوتی۔ میں اب وہاں جاؤں گی۔"

## ایمیلیا ایرہارٹ کے ساتھ بات چیت کریں

اگر آپ ایڈا کے ساتھ بات چیت کرنا چاہتے ہیں تو ، [حروف](/app/README.md) ایپ چلائیں۔

> [اہم!]
> 
> یہ مکمل طور پر خیالی ہے۔ جوابات اے آئی کے ذریعہ تیار کیے جاتے ہیں۔
> [ذمہ دار اے آئی ڈسکلیمر](/README.md#responsible-ai-disclaime)

<div>
  <img src="./assets/amelia-front.jpeg" alt="Ada Lovelace" width="300">
</div>

**اقدامات**:

1. شروع کریں [![GitHub Codespace](https://img.shields.io/badge/GitHub-Codespace-brightgreen)](https://codespaces.new/microsoft/generative-ai-with-javascript)
2. ریپو روٹ میں _/app_ پر جائیں۔
3. کنسول کو تلاش کریں اور`npm install` چلائیں جس کے بعد `npm start` چلیں۔
4. ایک بار جب یہ ظاہر ہوتا ہے تو ، "براؤزر میں کھولیں" بٹن منتخب کریں۔
5. امیلیا کے ساتھ بات چیت کریں.

ایپ کی مزید تفصیلی وضاحت کے لئے ، دیکھیں [تفصیلی ایپ وضاحت](/lessons/01-intro-to-genai/README.md#interact-with-dinocrates).

> [نوٹ!]
> 
 > اگر آپ اپنی مشین پر مقامی طور پر پروجیکٹ چلا رہے ہیں تو ، براہ کرم [گیٹ ہب ذاتی رسائی](/docs/setup/README.md#creating-a-personal-access-token-pat-for-github-model-access) ٹوکن سیٹ اپ حاصل کرنے کے لئے کوئیک اسٹارٹ گائیڈ کا جائزہ لیں اور کوڈ میں کلید کو تبدیل کریں۔

## ٹول کالنگ

**آپ**: "آلہ، ابھی کیا ہوا ہے؟"

**ٹائم بیٹل**: "آپ نے ابھی ایک آلے کو کال کیا ہے. ٹول ایک ایسا فنکشن ہے جسے اے آئی ماڈل کے ذریعہ کسی کام کو انجام دینے کے لئے بلایا جاسکتا ہے۔ آلے کو سادہ حساب کتاب سے لے کر پیچیدہ کارروائیوں تک ، کاموں کی ایک وسیع رینج انجام دینے کے لئے استعمال کیا جاسکتا ہے۔ اس معاملے میں ، آپ نے ایمیلیا ایرہارٹ کو مناسب لینڈنگ اسپاٹ تلاش کرنے میں مدد کرنے کے لئے 'فائنڈ لینڈنگ اسپاٹ' ٹول کا نام دیا۔"

**ٹائم بیٹل**: "ٹول کالنگ کے عمل کی وضاحت کرنے کے لئے یہاں ایک تصویر ہے:"

<div>
    <img src="./assets/tool_call_langchain.png" alt="Tool calling process illustration" width="600">
</div>


_ایمج کریڈٹ لینگ چین <https://python.langchain.com/docs/concepts/tool_calling/>_

**آپ**: اگر کچھ غلط ہو جائے تو کیا ہم غلطیوں سے نمٹ سکتے ہیں، جیسے کہ اگر آلے کو لینڈنگ کی جگہ نہیں مل سکتی ہے؟

**ٹائم بیٹل**: بہت اچھا سوال! جی ہاں، آپ اس طرح کے حالات کا انتظام کرنے کے لئے ایرر ہینڈلنگ شامل کرسکتے ہیں. مثال کے طور پر ، اگر ٹول لینڈنگ اسپاٹ تلاش کرنے میں ناکام ہوجاتا ہے تو ، آپ آگے بڑھنے سے پہلے ٹرائی کیچ بلاک استعمال کرسکتے ہیں یا نتیجہ چیک کرسکتے ہیں۔ فائنڈ لینڈنگ اسپاٹ ٹول کو کال کرتے وقت غلطیوں سے نمٹنے کی ایک مثال یہ ہے:

```javascript
try {
  const landingSpot = findLandingSpot(7.5, 134.5);
  if (!landingSpot) {
    throw new Error("No suitable landing spot found");
  }
  console.log(Landing spot found at coordinates: ${landingSpot.lat}, ${landingSpot.long});
} catch (error) {
  console.log(Error: ${error.message});
}
```

**آپ**: "میں ایک آلہ کیسے بناؤں؟"

**ٹائم بیٹل**: "ایک ٹول بنانے کے لئے، آپ کو ایک فنکشن کی وضاحت کرنے کی ضرورت ہے جو مطلوبہ کام انجام دیتا ہے. فنکشن کو ضروری ان پٹ لینا چاہئے اور آؤٹ پٹ کو واپس کرنا چاہئے۔ اس کے بعد آپ کام انجام دینے کے لئے اے آئی ماڈل سے فنکشن کال کرسکتے ہیں۔ یہاں 'فائنڈ لینڈنگ اسپاٹ' ٹول کیسا نظر آتا ہے:

```javascript
function findLandingSpot(lat, long) {
    // Perform the task of finding a suitable landing spot
    // Return the coordinates of the landing spot
    return { lat: 7.5, long: 134.5 };
}
```

**آپ**: "ٹھیک ہے، اے آئی ماڈل کو کیسے پتہ چلتا ہے کہ یہ آلہ موجود ہے؟"

**ٹائم بیٹل**: "آپ کو آلے کو اے آئی ماڈل کے ساتھ رجسٹر کرنے کی ضرورت ہے. یہ ماڈل کو بتاتا ہے کہ ٹول بلانے کے لئے دستیاب ہے۔ آئیے اگلے حصے میں اس کا احاطہ کرتے ہیں۔"

### ایک ٹول رجسٹر کرنا

**آپ**: "آپ نے کہا کہ مجھے آلے کو اے آئی ماڈل کے ساتھ رجسٹر کرنے کی ضرورت ہے. میں یہ کیسے کروں؟"

**ٹائم بیٹل**: "اے آئی ماڈل کے ساتھ ایک آلے کو رجسٹر کرنے کے لئے، آپ کو آلے کی میٹا ڈیٹا نمائندگی کی وضاحت کرنے کی ضرورت ہے. اس میٹا ڈیٹا میں آلے کا نام ، ان پٹ پیرامیٹرز ، اور آؤٹ پٹ فارمیٹ شامل ہونا چاہئے۔ اس کے بعد آپ میٹا ڈیٹا فراہم کرکے آلے کو اے آئی ماڈل کے ساتھ رجسٹر کرسکتے ہیں۔ 'فائنڈ لینڈنگ اسپاٹ' ٹول کے لئے میٹا ڈیٹا کی ایک مثال یہ ہے:

```json
{
  "name": "find-landing-spot",
  "description": "Finds a suitable landing spot",
  "parameters": {
    "type": "object",
    "properties": {
      "lat": {
        "type": "number",
        "description": "The latitude of the location",
      },
      "long": {
        "type": "number",
        "description": "The longitude of the location",
      },
    },
    "required": ["lat", "long"],
  },
  "output": { "type": "object", "properties": { "lat": "number", "long": "number" } }
}
```

**آپ**: "ٹھیک ہے، تو JSON کا ایک ٹکڑا ہے جو آلے کی وضاحت کرتا ہے، اب کیا؟"

**ٹائم بیٹل**: "اب، آپ کو اسے اپنے کلائنٹ چیٹ کی تکمیل کال پر اس طرح فراہم کرنے کی ضرورت ہے:

```javascript

function findLandingSpot(lat, long) {
    // Perform the task of finding a suitable landing spot
    // Return the coordinates of the landing spot
    return { lat: 7.5, long: 134.5 };
}

function getBackgroundOnCharacter(character) {
    // Perform the task of getting background information on a character
    // Return the background information
    return `Background information on ${character}`;
}

const getBackgroundOnCharacterJson = {
  name: "get-background-on-character",
  description: "Get background information on a character",
  parameters: {
    type: "object",
    properties: {
      name: {
        type: "string",
        description: "The name of the character",
      }
    },
    required: ["lat", "long"],
  },
  output: { type: "string" }
};

const findLandingSpotJson = {
  name: "find-landing-spot",
  description: "Finds a suitable landing spot",
  parameters: {
    type: "object",
    properties: {
      lat: {
        type: "number",
        description: "The latitude of the location",
      },
      long: {
        type: "number",
        description: "The longitude of the location",
      },
    },
    required: ["lat", "long"],
  },
  output: { type: "object", properties: { lat: "number", long: "number" } }
};


const messages = [{ 
    role: "user", 
    content: `Tell me about Amelia Earhart`,
}];

const completion = await openai.chat.completions.create({
    model: 'gpt-4o-mini',
    messages: messages,
    functions: [getBackgroundOnCharacterJson, findLandingSpotJson]
  });
```

**ٹائم بیٹل**: "پچھلے کوڈ کے ٹکڑے میں ہم:" 

- 'فائنڈ لینڈنگ اسپاٹ' ٹول اور 'گیٹ بیک گراؤنڈ آن کریکٹر' ٹول کے لیے میٹا ڈیٹا کی وضاحت کریں۔ 
- یہ میٹا ڈیٹا 'فنکشنز' پیرامیٹر کے حصے کے طور پر 'کلائنٹ ڈاٹ گیٹ چیٹ کمپلیشن' کال کو فراہم کریں۔ یہ اے آئی ماڈل کو بتاتا ہے کہ یہ ٹولز بلانے کے لئے دستیاب ہیں۔

**آپ**: "لہذا اے آئی ماڈل مناسب کال کرے گا اگر میں ایک اشارہ فراہم کرتا ہوں جو آلے کی وضاحت سے ملتا ہے؟"

**ٹائم بیٹل**: "تقریبا، یہ آپ کو بتائے گا کہ آپ کو کس ٹول کو کال کرنا چاہئے اور یہ آپ کو پارسڈ ان پٹ پیرامیٹرز فراہم کرے گا، لیکن آپ کو ٹول کو خود کال کرنے کی ضرورت ہے، میں آپ کو دکھاتا ہوں کہ کس طرح."

### ایک ٹول کال کرنا

**ٹائم بیٹل**: "جیسا کہ میں کہہ رہا تھا، اے آئی ماڈل آپ کو بتائے گا کہ اسے کون سا ٹول لگتا ہے کہ آپ کو کال کرنا چاہئے اور یہ آپ کو پارسڈ ان پٹ پیرامیٹرز فراہم کرے گا. اس کے بعد آپ کو آلے کو خود کال کرنے کی ضرورت ہے۔ یہاں ورک فلو قدم بہ قدم کیسا نظر آئے گا:

ٹول کال کو وائر اپ کریں

   سب سے پہلے ، آپ کو اپنے کوڈ میں ٹول کال کو وائر اپ کرنے کی ضرورت ہے۔ اس میں آلے کا فنکشن اور میٹا ڈیٹا نمائندگی بنانا شامل ہے ، اور پھر اے آئی ماڈل کو میٹا ڈیٹا فراہم کرنا شامل ہے۔

یوزر پرومپٹ کے ذریعہ ایک درخواست کرتا ہے:

   - پروگرام یوزر پرومپٹ اور ٹولز میٹا ڈیٹا فراہم کرنے کے ساتھ اے آئی ماڈل کو چیٹ کمپلیشن کی درخواست کرتا ہے۔
   - پروگرام کو ٹول کال کے ساتھ اے آئی ماڈل سے جواب ملتا ہے اور اگر اسے لگتا ہے کہ کسی ٹول کو بلایا جانا چاہئے تو ان پٹ پیرامیٹرز کو پارس کیا جاتا ہے۔
   - اگر ایسا ہے تو ، ڈویلپر جواب کی تشریح کرتا ہے اور اے آئی ماڈل کے ذریعہ فراہم کردہ فنکشن کال تجویز کی بنیاد پر ٹول کو استعمال کرتا ہے۔

**آپ**: "بہت اچھا، اب جب میں سمجھتا ہوں کہ کیا ہو رہا ہے، تو کیا آپ مجھے کچھ کوڈ دکھا سکتے ہیں؟"

**ٹائم بیٹل**: "یقینی طور پر، یہاں کوڈ وائر اپ ٹول کال ہے، چیٹ کمپلیشن کی درخواست کرتا ہے اور جواب کی تشریح کرتا ہے:

```javascript
import { OpenAI } from 'openai';
import { maybeCoerceInteger } from 'openai/core.mjs';

// 1: Define the function
function findLandingSpot(lat, long) {
  console.log("[Function] Finding landing spot with coordinates: ", lat, long);
  // Perform the task of finding a suitable landing spot
  // Return the coordinates of the landing spot
  return { lat: 7.5, long: 134.5 };
}

// 2: Define the tool metadata, should include description, parameters, and output
const findLandingSpotJson = {
  name: "find-landing-spot",
  description: "Finds a suitable landing spot",
  parameters: {
    type: "object",
    properties: {
      lat: {
        type: "number",
        description: "The latitude of the location",
      },
      long: {
        type: "number",
        description: "The longitude of the location",
      },
    },
    required: ["lat", "long"],
  },
  output: { type: "object", properties: { lat: "number", long: "number" } }
};

// 3: Add the tool to the tools object that we will use later to invoke the tool
const tools = {
  [findLandingSpotJson.name]: findLandingSpot
};

// 4: Create an instance of the OpenAI client
const openai = new OpenAI({
    baseURL: "https://models.inference.ai.azure.com", // might need to change to this url in the future: https://models.github.ai/inference
    apiKey: process.env.GITHUB_TOKEN,
});

// 5: Define the messages that will be sent to the AI model
const messages = [
{
    role: "system",
    content: `You are a helpful assistant. You can call functions to perform tasks. Make sure to parse the function call and arguments correctly.`
}, {
    role: "user",
    content: "Find a landing spot given coordinates 8.5, 130.5"
}
];

async function main(){
  console.log("Making LLM call")

  // 6: Call the AI model with the defined messages and tools
  const result = await openai.chat.completions.create({
      model: 'gpt-4o',
      messages: messages,
      functions: [findLandingSpotJson]
    });

  for (const choice of result.choices) {

      let functionCall = choice.message?.function_call;
      let functionName = functionCall?.name;
      let args = JSON.parse(functionCall?.arguments);

      // 7: Interpret response and call the tool based on the function call provided by the AI model
      if (functionName && functionName in tools) {
          console.log(`Calling [${functionName}]`);
          const toolFunction = tools[functionName];
          const toolResponse = toolFunction(...Object.values(args)); // Extract values from args and spread them
          console.log("Result from [tool] calling: ", toolResponse);
      }
  }
}

main();
```

پچھلے کوڈ میں ہم نے کہا ہے:

- 'فائنڈ لینڈنگ اسپاٹ' نامی ایک فنکشن بنایا جو ان پٹ کے طور پر طول بلد اور طول بلد لیتا ہے اور مناسب لینڈنگ اسپاٹ کے کوآرڈینیٹس کو واپس کرتا ہے۔
- 'فائنڈ لینڈنگ اسپاٹ' ٹول کے لئے میٹا ڈیٹا کی وضاحت کی.
- ایک 'ٹولز' آبجیکٹ بنایا جو ٹول میٹا ڈیٹا کو ٹول نیمز سے میپ کرتا ہے۔
- 'کلائنٹ ڈاٹ گیٹ چیٹ کمپلیشن ' کال پر 'ٹولز' آبجیکٹ فراہم کیا.
```javascript
if (functionName && functionName in tools) {
 console.log(`Calling [${functionName}]`);
 const toolFunction = tools[functionName];
 const toolResponse = toolFunction(...Object.values(args)); // Extract values from args and spread them
console.log("Result from [tool] calling: ", toolResponse);
}
```
- اے آئی ماڈل کے ذریعہ فراہم کردہ فنکشن کال کی بنیاد پر ٹول کال کیاجاتا ہے۔
- ٹول کال کا نتیجہ پرنٹ کیا.

**آپ**: "مجھے لگتا ہے کہ مجھے سمجھ آگیاہے. میں ایک فنکشن کی وضاحت کرتا ہوں ، ٹول کی میٹا ڈیٹا نمائندگی بناتا ہوں ، اے آئی ماڈل کو میٹا ڈیٹا فراہم کرتا ہوں ، اور پھر اے آئی ماڈل کے ذریعہ فراہم کردہ فنکشن کال کی بنیاد پر ٹول کو کال کرتا ہوں۔

**ٹائم بیٹل**: "بالکل! آپ اپنے ٹولز کی تعمیر شروع کرنے اور انہیں اے آئی ماڈل کے ساتھ ضم کرنے کے لئے تیار ہیں۔

## اسائنمنٹ - امیلیا کے ٹائم ٹریول ڈیوائس کو اپ گریڈ کریں

**ایمیلیا ایرہارٹ**: "خدا کا شکر ہے کہ لینڈنگ کی جگہ مل گئی. مضبوطی سے رہو!"

امیلیا ماہرانہ طور پر طیارے کو ایک چھوٹے سے جزیرے پر اتارتی ہے۔ آپ اور امیلیا ہوائی جہاز سے باہر نکلتے ہیں ، جس سے امیلیا آپ کو ایک چھوٹا سا آلہ دیتی ہے۔

**ایمیلیا ایرہارٹ**: "یہاں میری ڈیوائس ہے، آپ کی طرح فینسی نہیں ہے لیکن اس میں کچھ نفٹی خصوصیات ہیں. میں اس کا استعمال خود سفرکرنے کے لئے کر رہی ہوں۔ کیا آپ براہ مہربانی اسے میرے لئے اپ گریڈ کر سکتے ہیں؟"

**آپ**: "ٹائم بیٹل، کیا آپ امیلیا کے آلے کو اپ گریڈ کرنے میں میری مدد کرسکتے ہیں؟"

**ٹائم بیٹل**: "یقینا! امیلیا کے آلے کو اپ گریڈ کرنے کے لئے ، آئیے اس میں درج ذیل ٹولز شامل کریں:

- **ایک آلہ جو**: نقشے پر دو پوائنٹس کے درمیان فاصلے کا حساب لگائیں.
- **ایک آلہ جو**: GPS پوزیشن کا پتہ لگائیں جہاں امیلیا فی الحال واقع ہے.
- **ایک آلہ ہجو**: کسی مخصوص مقام کے لئے موسم کی پیشگوئی حاصل کرنے کے لئے بیرونی API کو کال کریں۔  

یہاں فنکشنز ہیں ، آپ کو صرف انہیں رجسٹر کرنے اور ان کی جانچ کرنے کی ضرورت ہے:

```javascript
function calculateDistance(lat1, long1, lat2, long2) {
    // Perform the task of calculating the distance between two points
    // Return the distance between the points
    return Math.sqrt((lat2 - lat1) ** 2 + (long2 - long1) ** 2);
}

function getGpsPosition() {
    // Perform the task of getting the GPS position of the current location
    // Return the GPS position
    return { lat: 7.5, long: 134.5 };
}

function getWeatherForecast(lat, long) {
    // Perform the task of getting the weather forecast for a given location
    // Return the weather forecast
    return "Sunny";
}
```

**آپ**: "ٹائم بیٹل، کیا آپ کو یقین ہے کہ یہ فنکشنز کام کرنے جا رہے ہیں، ایسا لگتا ہے کہ وہ صرف کچھ بے ترتیب اقدار واپس کر رہے ہیں؟"

**ٹائم بیٹل**: "یہ صحیح ہے، میں باقی کام اندرونی طور پر کر سکتا ہوں. آپ کو صرف انہیں رجسٹر کرنے اور ان کی جانچ کرنے کی ضرورت ہے ، اس بات کو یقینی بنائیں کہ اے آئی ماڈل انہیں کال کرسکے۔"

> ٹاسک: اے آئی ماڈل کے ساتھ کیلکولیٹ ڈسٹینس '، 'گیٹ جی پی ایس پوزیشن' اور 'گیٹ ویدر فارکاسٹ' ٹولز رجسٹر کریں۔ اے آئی ماڈل سے کال کرکے ٹولز کی جانچ کریں۔ پچھلے حصوں میں فراہم کردہ کوڈ کو حوالہ کے طور پر استعمال کریں۔

## حل

[حل](./solution/solution.js)

## علم کی جانچ پڑتال

**سوال:**  
اے آئی ماڈل کے ساتھ آلے کو رجسٹر کرنے کا مقصد کیا ہے؟

- اے آئی ماڈل کو ڈویلپر کی مداخلت کے بغیر آلے کو براہ راست انجام دینے کی اجازت دینا۔
- آلے کے بارے میں میٹا ڈیٹا فراہم کرنے کے لئے تاکہ اے آئی ماڈل اس کے استعمال کی تجویز دے سکے۔
- کوڈ میں فنکشنز کی وضاحت کی ضرورت کو تبدیل کرنا۔

**سوال:**  
ٹول کالنگ میں ٹول میٹا ڈیٹا کا کیا کردار ہے؟

- یہ اے آئی ماڈل کے لئے آلے کے مقصد ، ان پٹ اور آؤٹ پٹ کی وضاحت کرتا ہے۔
- یہ آلے کے نفاذ کی تفصیلات کے ساتھ اے آئی ماڈل فراہم کرتا ہے۔
- یہ اس بات کو یقینی بناتا ہے کہ آلے کو اے آئی ماڈل کے ذریعہ خود بخود انجام دیا جائے۔

**سوال:**  
ٹول کالنگ کا استعمال کیوں کریں؟

- اے آئی ماڈل کو بیرونی فنکشنز سے فائدہ اٹھاتے ہوئے اپنی بلٹ ان صلاحیتوں سے آگے کے کاموں کو انجام دینے کے قابل بنانا۔
- اے آئی ماڈل کی ترقی میں انسانی مداخلت کی ضرورت کو تبدیل کرنے کے لئے.
- اے آئی ماڈل کو میٹا ڈیٹا کی ضرورت کے بغیر ٹولز کو انجام دینے کی اجازت دینا۔

[حل کوئز](./solution/solution-quiz.md)

## خود مطالعہ کے وسائل

- [ٹول کالنگ کے عمل](https://learn.microsoft.com/en-us/semantic-kernel/concepts/ai-services/chat-completion/function-calling/?pivots=programming-language-csharp) کی وضاحت کرتا ہے
- [لین چین ڈاٹ جے ایس فریم ورک](https://js.langchain.com/docs/how_to/tool_calling/) میں ٹول کالنگ
- فنکشن کالنگ جیسا کہ [اوپن ائی لائبریری](https://github.com/openai/openai-node/blob/master/examples/function-call.ts) میں دکھایا گیا ہے
