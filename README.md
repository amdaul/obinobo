# Obinobo — ওয়েবসাইট

কিউরেটেড গিফট বক্স ব্র্যান্ড Obinobo-র সম্পূর্ণ মাল্টি-পেজ, মোবাইল-ফ্রেন্ডলি ওয়েবসাইট।

## ফাইল স্ট্রাকচার
```
index.html          → Home
products.html        → Products (তালিকা + ফিল্টার)
product.html         → একটা প্রোডাক্টের বিস্তারিত পেজ (?slug=budget-box বা ?slug=premium-box)
about.html           → About
contact.html         → Contact/Order (WhatsApp রিডাইরেক্ট সহ)
admin/               → Netlify CMS অ্যাডমিন প্যানেল (/admin)
data/products.json   → প্রোডাক্ট ডেটা (CMS দিয়ে এডিট হয়)
data/about.json      → About পেজের কনটেন্ট (CMS দিয়ে এডিট হয়)
data/settings.json   → WhatsApp নম্বর, Meta Pixel ID ইত্যাদি (CMS দিয়ে এডিট হয়)
images/              → SVG ছবি/আইকন (নিজের প্রোডাক্ট ছবি দিয়ে বদলে দিতে পারবেন)
css/style.css        → সব স্টাইল
js/main.js           → শেয়ার্ড লজিক (নেভিগেশন, অ্যানিমেশন, WhatsApp লিংক, ডেটা লোড)
js/chatbot.js        → জুমা চ্যাটবট (rule-based)
```

## Netlify-তে ডিপ্লয় করার ধাপ

1. এই পুরো ফোল্ডারটা একটা GitHub রিপোজিটরিতে পুশ করুন (অথবা Netlify-তে সরাসরি drag-and-drop ডিপ্লয় করতে পারেন — তবে drag-and-drop করলে অ্যাডমিন প্যানেল কাজ করবে না, কারণ Git Gateway-এর জন্য Git রিপো লাগে)।
2. [app.netlify.com](https://app.netlify.com)-এ গিয়ে "Add new site" → "Import an existing project" → আপনার GitHub রিপো সিলেক্ট করুন।
3. Build settings-এ কিছু বদলানোর দরকার নেই (এই সাইটে কোনো বিল্ড স্টেপ নেই, শুধু স্ট্যাটিক ফাইল)।
4. ডিপ্লয় হয়ে গেলে সাইটের নাম বদলে **obinobo** করুন (Site settings → Change site name), তাহলে লিংক হবে `obinobo.netlify.app`।

## অ্যাডমিন প্যানেল চালু করা (/admin)

1. Netlify ড্যাশবোর্ডে আপনার সাইটে যান → **Identity** ট্যাব → "Enable Identity" ক্লিক করুন।
2. Identity সেটিংসে **Registration** → "Invite only" সিলেক্ট করুন (যাতে শুধু আপনি লগইন করতে পারেন)।
3. **Services** → **Git Gateway** → "Enable Git Gateway" ক্লিক করুন।
4. Identity ট্যাব থেকে নিজেকে "Invite user" দিয়ে ইনভাইট করুন — ইমেইলে একটা লিংক পাবেন, সেটা দিয়ে পাসওয়ার্ড সেট করুন।
5. এরপর `obinobo.netlify.app/admin` এ গিয়ে লগইন করলেই প্রোডাক্ট, About কনটেন্ট ও সেটিংস (WhatsApp নম্বর, Meta Pixel ID) নিজে এডিট করতে পারবেন — কোনো কোড টাচ না করেই।

## প্রথমেই যা বদলাতে হবে

- `data/settings.json`-এ (বা /admin থেকে) `whatsappNumber` ফিল্ডে আপনার আসল WhatsApp নম্বর বসান (এখন placeholder `8801XXXXXXXXX` আছে)।
- `metaPixelId`-এ আপনার Facebook/Meta Pixel ID বসালে স্বয়ংক্রিয়ভাবে পুরো সাইটে ট্র্যাকিং পিক্সেল বসে যাবে।
- `images/logo.svg` নিজের লোগো দিয়ে বদলে দিন (একই নামে আপলোড করলে কোথাও কোড বদলাতে হবে না)।
- প্রোডাক্ট ছবিগুলো (`images/budget-box.svg`, `images/premium-box.svg`) এখন প্লেসহোল্ডার ইলাস্ট্রেশন — আসল প্রোডাক্ট ছবি দিয়ে বদলে দিতে পারেন /admin থেকে অথবা সরাসরি ফাইল আপলোড করে।

## কাস্টম ডোমেইন যোগ করা

Netlify-তে সাইট ডোমেইন কেনার পর: Site settings → Domain management → "Add a domain" থেকে যোগ করুন। কোনো কোড পরিবর্তনের দরকার নেই।

## কারিগরি নোট

- এটি একটি pure static সাইট (কোনো বিল্ড টুল/ফ্রেমওয়ার্ক নেই), তাই Netlify CMS-এর মাধ্যমে JSON ফাইল এডিট হলে সাইট তাৎক্ষণিক আপডেট দেখাবে (rebuild এর দরকার নেই, কারণ ডেটা রানটাইমে fetch হয়)।
- `product.html?slug=...` — এই একটা টেমপ্লেট পেজ দিয়েই সব প্রোডাক্টের আলাদা, শেয়ারযোগ্য লিংক তৈরি হয়। নতুন প্রোডাক্ট /admin থেকে যোগ করলে স্বয়ংক্রিয়ভাবে নতুন লিংক পাবে, কোনো নতুন HTML ফাইল বানাতে হবে না।
- জুমা চ্যাটবট সম্পূর্ণ rule-based (কোনো AI/API কল নেই) — তাই কোনো এক্সট্রা খরচ বা API key লাগবে না।
