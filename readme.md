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