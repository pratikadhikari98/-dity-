# ADITYA वेबसाइट — Setup README

## यो के हो
Static HTML/CSS/JS वेबसाइट हो — कुनै build step चाहिँदैन। सीधै फाइलहरू unzip गरेर deploy गर्न मिल्छ।

## फाइल संरचना
```
index.html          → गृहपृष्ठ (Hero + wheel, हाम्रो बारेमा short card, Result search modal, Lekh/History modal)
about.html           → बारेमा पेज (Features, Photo gallery, Showcase+YouTube+Social icons, Gravity-boxes, भर्ना CTA, Footer)
styles.css            → एउटै मात्र theme (खैरो/terracotta) — अरू theme फाइलहरू हटाइसकियो
photos/                → सबै images (logo, about photos, blackboard, sahitya-icon, आदि)
fonts/                  → Siddhanta custom font
manifest.json, icon-*.svg → PWA manifest + icons
sw.js (यदि छ भने)        → service worker (offline caching का लागि)
news/, results/, lekh.json → पुराना template बाट बचेका JSON data फाइलहरू (हाल प्रयोगमा: lekh.json — History modal ले पढ्छ)
```

## Deploy कसरी गर्ने
1. यो पूरै zip लाई Netlify, Vercel, GitHub Pages, वा जुनसुकै static hosting मा upload/drag-drop गर्नुहोस्।
2. `index.html` लाई root मा राख्नुहोस् — यो नै homepage हुनेछ।
3. कुनै पनि build command चाहिँदैन — यो पहिल्यै तयार (ready-to-deploy) HTML/CSS/JS हो।

## के-के हटाइयो (यस session मा)
- **Login / Firebase**: पूरै हटाइयो — header/hero बाट login button, र सबै Firebase (`firebase-app`, `firebase-auth`, `firebase-firestore`) script र JS function हरू (login, notices CRUD, comments, likes, community posts) — किनभने अब चाहिँदैन भनिएको थियो।
- **सूचना पाटी (कालोपाटी/Notices board)** र **समुदाय (Community posts)** section हरू — यी पूर्णतया Firebase-मा भर परेका थिए (backend बिना काम गर्दैनथे), त्यसैले हटाइयो।
- **थिम विकल्पहरू**: खैरो (terracotta) बाहेक अरू ५ थिम (black, blue, green, indigo, teal) का CSS फाइल र logo image variants — सबै हटाइयो। अब एउटै theme (styles.css) मात्र छ।

## के-के सारियो (index.html बाट about.html मा)
- Photo + text showcase, YouTube video cards, र Social icons (Facebook/Phone/Location active; YouTube/Instagram/Email अहिलेलाई "चाँडै आउँदैछ" — disabled, ID नआएसम्म)
- Gravity-boxes decorative animation section
- भर्ना (Admission) CTA section
- Footer (सम्पर्क जानकारी + copyright) — यो पहिल्यै about.html मा थियो, त्यसैले duplicate राखिएन, index.html बाट मात्र हटाइयो

**नोट**: `index.html` को Hero भित्रको "थप जान्नुहोस्" (History/Lekh modal) यथावत् index.html मा नै राखिएको छ, किनभने त्यसको button पनि Hero मै छ।

## Social icons मा link/नम्बर थप्ने वा बदल्ने
`about.html` भित्र `social-row` खोज्नुहोस् — त्यहाँ YouTube, Facebook, Instagram, Phone, Location, र Sahitya Sangrah का icon छन्।
- **YouTube/Instagram/Email** — हाल `disabled` class सहित निष्क्रिय छन्। ID आएपछि `<span class="social-icon disabled">` लाई `<a class="social-icon" href="...">` मा बदल्नुहोस्।
- **Phone** — `tel:9769312708` लाई आफ्नो नम्बरले replace गर्नुहोस्।
- **Location** — Google Maps link भित्रको query text बदल्नुहोस्।

## थप जानकारी
कुनै समस्या आए वा थप परिवर्तन चाहिएमा, यही zip भित्रका `index.html` / `about.html` / `styles.css` फाइल सिधै edit गरे पुग्छ — अरू कुनै tool/build प्रक्रिया चाहिँदैन।
# Results-hern-milne

## Admin Panel — website भित्रैबाट Showcase text/photo edit गर्ने (`admin.html`)
कुनै coding नगरी, browser बाटै showcase slides (text + photo) add/edit/delete गर्न सकिने page हो। यसले GitHub मा सिधै commit गर्छ — कुनै server/database चाहिँदैन।

**Setup (एकपटक मात्र):**
1. GitHub मा जानुहोस् → Settings → Developer settings → Personal access tokens → Fine-grained tokens → Generate new token।
2. यही repository छान्नुहोस्, अनि Permissions मा "Contents: Read and write" दिनुहोस्।
3. Token copy गर्नुहोस् (यो एकपटक मात्र देखिन्छ)।

**प्रयोग गर्ने तरिका:**
1. `yoursite.com/admin.html` खोल्नुहोस्।
2. Token, GitHub username (owner), repository नाम, र branch (प्रायः `main`) भर्नुहोस् — यो browser मै save हुन्छ, फेरि भर्नु पर्दैन।
3. "Load गर्नुहोस्" थिच्नुहोस् — अहिलेका सबै slide देखिन्छन्।
4. जुनसुकै slide को text/photo edit गर्नुहोस्, नयाँ थप्न "+ नयाँ Slide थप्नुहोस्" थिच्नुहोस्, हटाउन "हटाउनुहोस्" थिच्नुहोस्।
5. "GitHub मा Save गर्नुहोस्" थिच्नुहोस् — यसले नयाँ फोटो (यदि छ भने) `photos/` मा अपलोड गर्छ अनि `data/showcase.json` अपडेट गरी सिधै GitHub मा commit गर्छ।
6. केही मिनेटमा (Netlify/hosting rebuild हुँदा) वेबसाइटमा परिवर्तन देखिन्छ।

**कहाँ data बस्छ:**
- `data/showcase.json` — Showcase carousel (photo+text), `index.html` र `about.html` दुबैमा
- `data/shlokas.json` — Hero (wheel को साइड) मा देखिने श्लोक + अर्थ; एकभन्दा बढी राख्नुभयो भने हरेक ५ सेकेन्डमा अर्को श्लोक देखिन्छ
- `data/about.json` — Homepage को "हाम्रो बारेमा" card को text
- `data/news.json` — About page को समाचार section (🗞️ icon, /about.html#news) — title + text + रङ (color) + featured फोटो, जति पनि समाचार थप्न मिल्छ। Text भित्र जुनसुकै ठाउँमा जति पनि फोटो पनि राख्न मिल्छ (admin.html को "फोटो यहाँ थप्नुहोस्" बटनले cursor भएको ठाउँमा नै फोटो insert गर्छ)। Mobile/desktop दुवैमा 3-column newspaper layout मा देखिन्छ।

यी सबै फाइल directly पनि edit गर्न मिल्छ (कुनै text editor बाट), वा admin.html बाट।

⚠️ **सुरक्षा नोट**: `admin.html` लाई link नगर्नुहोस् (header/footer मा नराख्नुहोस्) — जसलाई URL थाहा छ उसैले मात्र प्रयोग गरून् भन्नका लागि। Token आफ्नै मात्र भएको browser मा राख्नुहोस्, अरूसँग share नगर्नुहोस्।

