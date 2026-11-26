APNA FUND – FIREBASE ADMIN PREVIEW

इस build में Firebase Email/Password Admin login और Firestore पर Admin-only cloud backup का प्रारंभिक जोड़ है। यह अभी 10 सदस्यों का अलग-अलग login/member portal या individual online loan voting नहीं है।

जरूरी सेटअप (कंप्यूटर पर करना आसान होगा):
1) Firebase Console > Authentication > Users > Add user में अपना Admin email और मजबूत password बनाएं।
2) बने हुए user का UID कॉपी करें।
3) firebase-config.js में ADMIN_UID की जगह वही UID डालें।
4) firestore.rules में भी PASTE_ADMIN_UID_HERE की जगह वही UID डालें। Firestore > Rules में पूरा rules content paste करके Publish करें।
5) पूरा folder HTTPS hosting पर upload करें (सिर्फ index.html खोलने से module imports काम नहीं करेंगे)।
6) ऐप खोलकर उसी Admin email/password से login करें।

सुरक्षा: Rules में सिर्फ उस UID को groupData/main पढ़ने/लिखने की अनुमति है। बाकी सब deny है। किसी भी दूसरे UID को Admin न बनाएं। Firebase web apiKey client config है; Service Account JSON/private key कभी साझा न करें।

महत्वपूर्ण सीमाएँ:
- इस चरण में cloud document Admin-only है; members को login न दें।
- Member-wise access, member profiles/ledger, individually authenticated loan votes, secure file storage, audit log और server-side validation अगला चरण हैं।
- पुराना localStorage डेटा cloud में पहली Admin login पर migrate हो सकता है; पहले backup JSON डाउनलोड रखें।
- इस prototype को असली जमा/लोन संचालन में तब तक उपयोग न करें जब तक member access controls और legal/financial checks पूरे न हों।
- Firestore usage free quota से ऊपर जाने पर charges हो सकते हैं; billing alert लगाएं।
