# KMJ TIPS Toast Module — FULL SETUP GUIDE

Pura system 3 hisso me hai: **BOT** (control) + **DEX** (app ke andar) + **HOOK** (ek line).
Config.json / GitHub / database — kuch nahi chahiye. Config bot ke paas
rehta hai (owner ki chat me pinned message).

═══════════════════════════════════════════
STEP 1 — BOT HOST KARO (Vercel)
═══════════════════════════════════════════
1. Vercel pe naya project banao.
2. Files aise rakho:
       api/bot.py          ← bot/kmj_toast_bot.py (naam bot.py ya index.py, koi bhi)
       vercel.json         ← project root me
       requirements.txt    ← project root me
3. Env vars me SIRF 2 cheezein dalo:
       BOT_TOKEN = BotFather wala token
       OWNER_ID  = tumhari numeric Telegram ID
4. Deploy karo.
5. Webhook set karo (browser me ek baar ye link kholo):
       https://api.telegram.org/bot<TOKEN>/setWebhook?url=https://<project>.vercel.app/api/bot
   (file ka naam index.py rakha ho to link me /api/index aayega)
6. Bot pe /start bhejo → panel aayega. Bot khud ek ⚙️ CONFIG STORAGE
   message pin kar dega — use delete/unpin mat karna.

═══════════════════════════════════════════
STEP 2 — DEX ADD KARO
═══════════════════════════════════════════
kmj-tips-toast.dex ko apne app ke build me agle khali number se rakho:
classes2.dex / classes3.dex / classes4.dex — jo number khali ho.

═══════════════════════════════════════════
STEP 3 — HOOK CODE (launcher Activity ke onCreate me)
═══════════════════════════════════════════
Default host (kmj-toast-bot.vercel.app) ke liye 1 line:
    invoke-static {p0}, Lcom/kmjtips/toast/KmjToast;->init(Landroid/content/Context;)V

Apna alag host ho to 2 line wala (apna ?config link do):
    const-string v0, "https://<tumhara-host>/api/bot?config"
    invoke-static {p0, v0}, Lcom/kmjtips/toast/KmjToast;->init(Landroid/content/Context;Ljava/lang/String;)V

Build karke install karo — ho gaya. ✔

═══════════════════════════════════════════
BOT SE CONTROL (panel buttons + commands)
═══════════════════════════════════════════
🟢 Normal Mode    → sabke liye normal dialog (force pura saaf)
🔴 Force Update   → sirf Update Now, app lock
⚫ Dialog OFF / 🟢 Dialog ON
✏️ Text Edit      → abhi ka text dekho, naya /text <message> se lagao
🗑 Text Delete     → text delete + box hide
👁 Text Show ON/OFF → text box dikhana / chhupana
📢 Announcement   → /announce <text> bhejo, /announce off band
/status           → abhi ka mode   |   /config → pura config
/expire 2026-12-31 → us date ke baad Expired screen

Note: ek button dabane ke baad 20-30 second ruko (app har 20 sec check
karta hai). Tez-tez taps mat karna.
