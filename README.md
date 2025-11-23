# 🧳 Travel Planner Bot  
**LLM-Powered Travel Planning Application Using Streamlit, OpenAI, Google Colab, and ngrok**

This project is a bilingual (Arabic + English) travel planner powered by a Large Language Model (LLM).  
The system generates complete travel itineraries based on user inputs such as destination, duration, budget, traveler type, and interests.

The application was built as part of the **Selected Topics** course at Almaarefa University – Computer Science & Information Systems Department.

---

## 🚀 Features

### 🌍 Bilingual Interface
- Arabic 🇸🇦  
- English 🇬🇧  

### 🧠 AI-Powered Travel Planning
Automatically generates:
- Trip overview  
- Day-by-day itinerary  
- Hotel recommendations  
- Budget breakdown  
- Restaurants & cafes  
- Attractions  
- Travel tips  
- Packing checklist  

### 🎨 Professional UI Design
- Dark mode  
- Modern CSS theme  
- Gradient button  
- Organized layout  
- Badges for technologies  

### ☁️ Works Fully Through Google Colab
- No local installation  
- Uses `streamlit` for UI  
- Uses `ngrok` for public web access  

---

## 🛠️ Technologies Used

| Component | Technology |
|----------|------------|
| Frontend | Streamlit |
| Backend | Python |
| LLM | OpenAI GPT-4o-mini |
| Deployment (dev) | Google Colab |
| Public Access | ngrok tunnel |
| Styling | Custom CSS |

---

## 📦 Folder Structure

1) Install required packages
```bash
!pip install streamlit
!pip install pyngrok
```

2) Add OpenAI API Key
```python
import os
os.environ["OPENAI_API_KEY"] = "YOUR_OPENAI_KEY"
```


3)Add ngrok Token
```python
from pyngrok import ngrok
ngrok.set_auth_token("35i3tMXEW10EmwqH9bu296cji3k_2ttMH9ifk71EmQ9ykxnVv")
```

4)Create the Application File
```python
%%writefile app.py 
import streamlit as st
from openai import OpenAI
import os

# === إعداد عميل OpenAI ===
client = OpenAI(api_key=os.environ["OPENAI_API_KEY"])

# === إعداد الصفحة ===
st.set_page_config(
    page_title="Travel Planner Bot",
    page_icon="🧳",
    layout="wide",
)

# === CSS مخصص للتصميم الاحترافي ===
st.markdown("""
<style>
.stApp {
    background: #020617;
    color: #e5e7eb;
    font-family: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
}
.main .block-container {
    padding-top: 2.5rem;
    padding-bottom: 3rem;
    max-width: 1100px;
}
h1, h2, h3, h4 {
    color: #f9fafb;
}
small, .caption {
    color: #9ca3af !important;
}
.card {
    background: #020617;
    border: 1px solid #1f2937;
    border-radius: 16px;
    padding: 1.5rem 1.8rem;
    margin-bottom: 1.5rem;
    box-shadow: 0 18px 40px rgba(15,23,42,0.55);
}
.sub-card {
    background: #020617;
    border: 1px solid #1f2937;
    border-radius: 14px;
    padding: 1.25rem 1.5rem;
    margin-top: 0.5rem;
    margin-bottom: 1.2rem;
}
.stRadio > label, .stSelectbox > label, .stSlider > label,
.stTextInput > label, .stMultiselect > label, .stTextArea > label {
    font-weight: 600;
    color: #e5e7eb;
}
.stTextInput>div>div>input,
.stSelectbox>div>div>select,
.stMultiselect>div>div>div>div,
.css-1cypcdb, .stSlider > div > div {
    background-color: #020617 !important;
    color: #e5e7eb !important;
}
.stSlider > div > div > div[data-baseweb="slider"] > div {
    background-color: #f97316 !important;
}
.stButton>button {
    background: linear-gradient(135deg, #2563eb, #7c3aed);
    color: white;
    border-radius: 999px;
    padding: 0.6rem 1.8rem;
    font-weight: 600;
    border: none;
    box-shadow: 0 10px 25px rgba(37,99,235,0.45);
}
.stButton>button:hover {
    background: linear-gradient(135deg, #1d4ed8, #6d28d9);
    transform: translateY(-1px);
}
.badge {
    display: inline-block;
    padding: 0.15rem 0.55rem;
    border-radius: 999px;
    font-size: 0.72rem;
    background: rgba(148,163,184,0.18);
    color: #e5e7eb;
    border: 1px solid rgba(148,163,184,0.35);
    margin-right: 0.4rem;
}
.section-title {
    font-size: 0.78rem;
    text-transform: uppercase;
    letter-spacing: 0.09em;
    color: #9ca3af;
    font-weight: 700;
}
</style>
""", unsafe_allow_html=True)

# === اختيار اللغة ===
lang = st.radio("Language / اللغة", ["English", "العربية"], horizontal=True)

def t(ar, en):
    return ar if lang == "العربية" else en

# === الهيدر ===
with st.container():
    col_logo, col_title = st.columns([1, 5])
    with col_logo:
        st.markdown("## 🧳")
    with col_title:
        st.markdown(
            t("## مساعد تخطيط السفر", "## Travel Planner Bot"),
            help=t("مساعد ذكي لبناء خطة سفر مخصّصة.", "An intelligent assistant for personalized trip planning.")
        )
        st.markdown(
            t(
                "أنشئ خطة سفر متكاملة حسب الوجهة، عدد الأيام، الميزانية ونوع المسافر.",
                "Generate a complete trip plan based on destination, duration, budget and traveler type."
            )
        )
    st.markdown(
        '<span class="badge">LLM-powered</span><span class="badge">Streamlit</span><span class="badge">Riyadh Example</span>',
        unsafe_allow_html=True,
    )

st.markdown("")

# === كارت إعدادات الرحلة ===
st.markdown(f'<div class="card">', unsafe_allow_html=True)
st.markdown(f'<div class="section-title">{t("إعداد الرحلة", "Trip configuration")}</div>', unsafe_allow_html=True)
st.markdown("")

col_left, col_right = st.columns(2)

with col_left:
    destination = st.text_input(
        t("الوجهة", "Destination"),
        value="Riyadh" if lang == "English" else "الرياض",
        placeholder=t("مثال: الرياض، دبي، باريس...", "e.g., Riyadh, Dubai, Paris..."),
    )
    days = st.slider(
        t("عدد الأيام", "Trip duration (days)"),
        min_value=1,
        max_value=30,
        value=5,
    )
    budget = st.selectbox(
        t("مستوى الميزانية", "Budget level"),
        [t("منخفضة", "Low"), t("متوسطة", "Medium"), t("مرتفعة", "High")],
        index=1,
    )

with col_right:
    traveler = st.selectbox(
        t("نوع المسافر", "Traveler type"),
        [t("مسافر فردي", "Solo"), t("عائلة", "Family"), t("أصدقاء", "Friends"), t("عمل / بزنس", "Business")],
    )
    interests = st.multiselect(
        t("الاهتمامات", "Interests"),
        [
            t("تسوق", "Shopping"),
            t("طبيعة", "Nature"),
            t("طعام", "Food"),
            t("ثقافة وتاريخ", "Culture & History"),
            t("مغامرات", "Adventure"),
        ],
        default=[t("تسوق", "Shopping"), t("طعام", "Food")],
    )

notes = st.text_area(
    t("ملاحظات إضافية (اختياري)", "Additional notes (optional)"),
    placeholder=t(
        "مثال: أفضّل أماكن مناسبة للعائلة والأطفال – لا أرغب في الأنشطة الخطرة.",
        "Example: Prefer family-friendly places – no extreme activities.",
    ),
)

st.markdown("</div>", unsafe_allow_html=True)

# === زر التخطيط ===
st.markdown("")
center_col = st.columns([2, 1, 2])[1]
with center_col:
    generate = st.button(t("✨ خطِّط رحلتي", "✨ Plan my trip"))

# === منطقة عرض الخطة ===
st.markdown("")
st.markdown(f'<div class="card">', unsafe_allow_html=True)
st.markdown(f'<div class="section-title">{t("خطة السفر الناتجة", "Generated travel plan")}</div>', unsafe_allow_html=True)
st.markdown("")

if generate:
    if not destination.strip():
        st.warning(t("رجاءً أدخل وجهة أولاً.", "Please enter a destination first."))
    else:
        with st.spinner(t("جاري إنشاء خطة الرحلة...", "Generating your travel plan...")):
            interests_text = ", ".join(interests) if interests else t("لم يتم التحديد", "Not specified")

            if lang == "العربية":
                user_prompt = f"""
الوجهة: {destination}
مدة الرحلة (أيام): {days}
مستوى الميزانية: {budget}
نوع المسافر: {traveler}
الاهتمامات: {interests_text}
ملاحظات إضافية: {notes}

أنت مساعد تخطيط سفر محترف، أنشئ خطة مفصلة باللغة العربية فقط.

رجاءً أعِد النتيجة بالتنسيق التالي (Markdown):

1. **نظرة عامة عن الرحلة**
2. **خطة يومية لكل يوم (صباحًا / ظهرًا / مساءً)**
3. **خيارات الفنادق (فاخر – متوسط – اقتصادي)**
4. **جدول تقديري للميزانية**
5. **أفضل المطاعم والمقاهي**
6. **أهم المعالم والأنشطة**
7. **نصائح وتذكيرات قبل وأثناء السفر**
8. **قائمة تجهيز السفر (Checklist)**

لا تذكر أنك نموذج ذكاء اصطناعي.
"""
            else:
                user_prompt = f"""
Destination: {destination}
Trip duration: {days}
Budget level: {budget}
Traveler type: {traveler}
Interests: {interests_text}
Additional notes: {notes}

You are a professional travel planning assistant.

Return a detailed travel plan in **English only** with:
1. Trip overview
2. Day-by-day itinerary
3. Hotels (luxury / mid-range / budget)
4. Budget breakdown
5. Restaurants
6. Attractions
7. Tips
8. Packing checklist
"""

            try:
                response = client.chat.completions.create(
                    model="gpt-4o-mini",
                    messages=[
                        {"role": "system", "content": "You are a helpful and structured travel planner."},
                        {"role": "user", "content": user_prompt},
                    ],
                    temperature=0.7,
                )
                plan_text = response.choices[0].message.content
                st.markdown(plan_text)

            except Exception as e:
                st.error(t("حدث خطأ أثناء الاتصال بالذكاء الاصطناعي.", "An error occurred while contacting the AI model."))
                st.exception(e)

else:
    st.markdown(
        t(
            "اضغط زر «خطط رحلتي» بعد تعبئة البيانات.",
            "Press “Plan my trip” after filling the form."
        )
    )

st.markdown("</div>", unsafe_allow_html=True)
```

5) Start Tunnel
```python
public_url = ngrok.connect(8501)
public_url
```
6) Run Streamlit
```bash
!streamlit run app.py --server.address 0.0.0.0 --server.port 8501
```
