import streamlit as st
import graphviz

# إعدادات الصفحة للحصول على مظهر حديث وعريض
st.set_page_config(page_title="شجرة العناصر الإنشائية", page_icon="🏗️", layout="wide")

# تصميم الهيدر (Header) باستخدام HTML و CSS مخصص
st.markdown("""
    <div style="background-color: #1E3A8A; padding: 20px; border-radius: 10px; margin-bottom: 30px;">
        <h1 style="color: white; text-align: center; font-family: 'Cairo', sans-serif;">🏗️ دليل عائلة العناصر الإنشائية للخرسانة المسلحة</h1>
        <p style="color: #E2E8F0; text-align: center; font-size: 1.1rem;">شجرة تفاعلية تمثل الهيكل الإنشائي للمباني بتنسيق بصري حديث</p>
    </div>
""", unsafe_allow_html=True)

# إنشاء كائن الرسم (Graph) مع إضافة خصائص المظهر الحديث والألوان
dot = graphviz.Digraph(comment='Structural Elements Tree')

# إعدادات التصميم العام للرسم (توجيه من اليمين لليسار، ونوع الخط، والخلفية)
dot.attr(
    rankdir='LR',  # عرض الشجرة من اليسار إلى اليمين (مناسب للشاشات العريضة)
    fontname='Arial',
    size='12,12',
    bgcolor='#F8FAFC'  # خلفية مريحة للعين
)

# تعريف أنماط العقد (Nodes) بناءً على مستواها في الشجرة (لوحة ألوان حديثة)
styles = {
    'root': {'shape': 'box', 'style': 'filled', 'color': '#1E3A8A', 'fillcolor': '#1E3A8A', 'fontcolor': 'white', 'fontsize': '16', 'penwidth': '3'},
    'level1': {'shape': 'box', 'style': 'filled,rounded', 'color': '#0284C7', 'fillcolor': '#0EA5E9', 'fontcolor': 'white', 'fontsize': '14', 'penwidth': '2'},
    'level2': {'shape': 'ellipse', 'style': 'filled', 'color': '#0D9488', 'fillcolor': '#14B8A6', 'fontcolor': 'white', 'fontsize': '12'},
    'leaf': {'shape': 'note', 'style': 'filled', 'color': '#475569', 'fillcolor': '#F1F5F9', 'fontcolor': '#1E293B', 'fontsize': '11'}
}

# خصائص الخطوط الموصلة (Edges)
edge_attr = {'color': '#94A3B8', 'arrowsize': '0.7', 'penwidth': '1.5'}

# 1. العقدة الرئيسية (Root)
dot.node('root', '🏢 الهيكل الإنشائي\n(Structure)', **styles['root'])

# 2. المستوى الأول (التصنيفات الرئيسية)
dot.node('sub', '🪵 1. الأساسات وتحت الأرض\n(Substructure)', **styles['level1'])
dot.node('super', '🏗️ 2. الهيكل العلوي\n(Superstructure)', **styles['level1'])
dot.node('circ', '🧗 3. عناصر الحركة\n(Circulation)', **styles['level1'])
dot.node('spec', '💧 4. المنشآت الخاصة\n(Special)', **styles['level1'])

# ربط المستوى الأول بالرئيسي
dot.edge('root', 'sub', **edge_attr)
dot.edge('root', 'super', **edge_attr)
dot.edge('root', 'circ', **edge_attr)
dot.edge('root', 'spec', **edge_attr)

# 3. تفريع قسم الأساسات (Substructure)
dot.node('sub_shallow', '📐 الأساسات السطحية', **styles['level2'])
dot.node('sub_deep', '🕳️ الأساسات العميقة', **styles['level2'])
dot.node('sub_ties', '⛓️ عناصر الربط الأرضي', **styles['level2'])

dot.edge('sub', 'sub_shallow', **edge_attr)
dot.edge('sub', 'sub_deep', **edge_attr)
dot.edge('sub', 'sub_ties', **edge_attr)

# أوراق الأساسات السطحية
dot.node('isolated', '⏹️ القواعد المنفصلة', **styles['leaf'])
dot.node('combined', '🔗 القواعد المشتركة', **styles['leaf'])
dot.node('strip', '🧱 القواعد الشريطية', **styles['leaf'])
dot.node('raft', '🌊 اللبشة / الحصيرة', **styles['leaf'])
dot.edge('sub_shallow', 'isolated', **edge_attr)
dot.edge('sub_shallow', 'combined', **edge_attr)
dot.edge('sub_shallow', 'strip', **edge_attr)
dot.edge('sub_shallow', 'raft', **edge_attr)

# أوراق الأساسات العميقة
dot.node('piles', '🪵 الخوازيق الخرسانية', **styles['leaf'])
dot.node('pile_caps', '🎚️ هامات الخوازيق', **styles['leaf'])
dot.edge('sub_deep', 'piles', **edge_attr)
dot.edge('sub_deep', 'pile_caps', **edge_attr)

# أوراق عناصر الربط الأرضي
dot.node('grade_beams', '➖ الميدات الأرضية', **styles['leaf'])
dot.node('ret_basement', '🧱 جدران القبو الاستنادية', **styles['leaf'])
dot.edge('sub_ties', 'grade_beams', **edge_attr)
dot.edge('sub_ties', 'ret_basement', **edge_attr)


# 4. تفريع قسم الهيكل العلوي (Superstructure)
dot.node('sup_vert', '📐 العناصر الرأسية\n(الضغط)', **styles['level2'])
dot.node('sup_horiz', '📐 العناصر الأفقية\n(الانحناء)', **styles['level2'])

dot.edge('super', 'sup_vert', **edge_attr)
dot.edge('super', 'sup_horiz', **edge_attr)

# أوراق العناصر الرأسية
dot.node('columns', '🏛️ الأعمدة\n(دائرية / مستطيلة)', **styles['leaf'])
dot.node('shear_walls', '🧱 حوائط القص\n(الزلازل)', **styles['leaf'])
dot.node('core_walls', '🛗 جدران بئر المصعد', **styles['leaf'])
dot.edge('sup_vert', 'columns', **edge_attr)
dot.edge('sup_vert', 'shear_walls', **edge_attr)
dot.edge('sup_vert', 'core_walls', **edge_attr)

# أوراق العناصر الأفقية
dot.node('beams', '桥 الكمرات / الجسور\n(ساقطة/مقلوبة/مدفونة)', **styles['leaf'])
dot.node('slabs', '🥞 البلاطات / الأسقف\n(مصمتة/لاكمرية/هوردي)', **styles['leaf'])
dot.edge('sup_horiz', 'beams', **edge_attr)
dot.edge('sup_horiz', 'slabs', **edge_attr)


# 5. أوراق عناصر الحركة (Circulation)
dot.node('stairs', '🦿 السلالم الخرسانية', **styles['leaf'])
dot.node('ramps', '🎢 المنحدرات الخرسانية', **styles['leaf'])
dot.edge('circ', 'stairs', **edge_attr)
dot.edge('circ', 'ramps', **edge_attr)


# 6. أوراق المنشآت الخاصة (Special)
dot.node('tanks', '🪣 خزانات المياه', **styles['leaf'])
dot.node('pools', '🏊 حمامات السباحة', **styles['leaf'])
dot.edge('spec', 'tanks', **edge_attr)
dot.edge('spec', 'pools', **edge_attr)

# عرض الشجرة داخل تطبيق Streamlit مع تفعيل التكبير والتصغير التفاعلي
st.graphviz_chart(dot, use_container_width=True)

# إضافة تلميح للمستخدم في الأسفل
st.caption("💡 نصيحة: يمكنك تكبير وتصغير الشجرة، أو سحبها، أو الضغط على زر ملء الشاشة المدمج في الزاوية العلوية للرسم لرؤية التفاصيل بوضوح.")
