# เว็บไซต์สโมสรฟุตบอลลิเวอร์พูล (Liverpool FC Website)

เว็บไซต์นี้สร้างขึ้นเพื่อแฟนบอลลิเวอร์พูล (The Kop) โดยนำเสนอข้อมูลเกี่ยวกับสโมสร, เหตุการณ์สำคัญ, รายชื่อผู้เล่นชุดปัจจุบัน และถ้วยรางวัลต่างๆ พัฒนาด้วย Flask, HTML และ CSS

## คุณสมบัติหลัก (Features)

*   **หน้าแรก (Home):** แสดงข้อความต้อนรับและไฮไลท์เหตุการณ์สำคัญในประวัติศาสตร์ของลิเวอร์พูล
*   **หน้ารายชื่อผู้เล่น (Squad):** แสดงรายชื่อผู้เล่นชุดปัจจุบัน พร้อมรูปภาพและหมายเลขเสื้อ
*   **เหตุการณ์สำคัญ (Memorable Moments):** รวบรวมเหตุการณ์สำคัญที่น่าจดจำ พร้อมลิงก์ไปยังวิดีโอ YouTube ที่เกี่ยวข้อง
*   **แสดงถ้วยรางวัล (Trophy Display):** แสดงภาพถ้วยรางวัล
*   **ระบบยืนยันตัวตนผู้ใช้ (User Authentication):** รองรับการลงทะเบียน, เข้าสู่ระบบ และออกจากระบบ (ต้องมีโค้ด Flask เพิ่มเติม)
*   **แดชบอร์ด (Dashboard):** หน้าสำหรับผู้ใช้ที่เข้าสู่ระบบแล้วเท่านั้น (ต้องมีโค้ด Flask เพิ่มเติม)
*   **การเลื่อนหน้าจออย่างนุ่มนวล (Smooth Scrolling):** ใช้ JavaScript เพื่อเลื่อนไปยังส่วนต่างๆ ของหน้าเว็บอย่างนุ่มนวล

## เทคโนโลยีที่ใช้ (Technologies Used)

*   **Flask:** เฟรมเวิร์กเว็บขนาดเล็ก (Micro Web Framework) ที่เขียนด้วยภาษา Python (ต้องติดตั้งและเขียนโค้ดเพิ่มเติม)
*   **HTML:** ใช้สำหรับโครงสร้างหน้าเว็บ
*   **CSS:** ใช้สำหรับตกแต่งหน้าเว็บ
*   **JavaScript:** ใช้สำหรับเพิ่มลูกเล่น เช่น การเลื่อนหน้าจออย่างนุ่มนวล

## โครงสร้างโปรเจ็กต์ (Project Structure)

โครงสร้างของโปรเจ็กต์ถูกจัดระเบียบดังนี้:

*   `static/`: โฟลเดอร์สำหรับไฟล์ static เช่น CSS และรูปภาพ
    *   `css/`: โฟลเดอร์สำหรับไฟล์ `style.css` (คุณต้องสร้างไฟล์นี้และใส่ CSS code เอง)
    *   `images/`: โฟลเดอร์สำหรับรูปภาพที่ใช้ในเว็บไซต์ (โลโก้, ผู้เล่น, ถ้วยรางวัล, ฯลฯ)
*   `templates/`: โฟลเดอร์สำหรับไฟล์ HTML templates
    *   `base.html`: Template หลักที่เป็นโครงสร้างพื้นฐานของทุกหน้า
    *   `dashboard.html`: Template สำหรับแดชบอร์ดของผู้ใช้ (ต้องมีโค้ด Flask เพิ่มเติม)
    *   `index.html`: Template สำหรับหน้าแรก

## คำอธิบายโค้ด (Code Explanation)

### `base.html`

ไฟล์นี้เป็น template หลักสำหรับทุกหน้าในเว็บไซต์ ประกอบด้วย:

*   **`<head>`:**
    *   กำหนด charset และ viewport
    *   ตั้งค่า title ของหน้าเว็บ (ใช้ `{% block title %}{% endblock %}` เพื่อให้แต่ละหน้าสามารถกำหนด title ของตัวเองได้)
    *   ลิงก์ไปยังไฟล์ CSS (`style.css`) ในโฟลเดอร์ `static/css/`
    *   ลิงก์ไปยัง favicon (ไอคอนเล็กๆ ที่แสดงใน tab ของ browser)
    *   กำหนด style สำหรับระยะห่างระหว่างลิงก์ใน navigation bar
*   **`<nav>`:**
    *   สร้าง navigation bar ด้านบนของหน้าเว็บ
    *   มีโลโก้และชื่อสโมสร (Liverpool FC) ที่ลิงก์ไปยังหน้าแรก (`/`)
    *   มีลิงก์ไปยังส่วน "Memorable Things", "Player" (Squad), และ "Trophy" โดยใช้ JavaScript functions (`scrollToMemorable()`, `scrollToSquad()`, `scrollToTrophy()`) เพื่อเลื่อนหน้าจอไปยังส่วนนั้นๆ อย่างนุ่มนวล
    *   มีลิงก์สำหรับ Login, Register, Dashboard, และ Log Out โดยจะแสดงลิงก์ที่แตกต่างกันขึ้นอยู่กับว่าผู้ใช้ได้ login หรือยัง (ใช้ `{% if current_user.is_authenticated %}` ในการตรวจสอบ)
*   **`{% block content %}{% endblock %}`:**
    *   ส่วนนี้เป็น placeholder สำหรับเนื้อหาของแต่ละหน้า (content ที่จะแตกต่างกันในแต่ละหน้า)
*   **`<script>`:**
    *   มี JavaScript functions (`scrollToMemorable()`, `scrollToSquad()`, `scrollToTrophy()`) สำหรับเลื่อนหน้าจออย่างนุ่มนวลไปยังส่วนต่างๆ ของหน้าเว็บ

### `index.html`

ไฟล์นี้เป็น template สำหรับหน้าแรกของเว็บไซต์ ประกอบด้วย:

*   **`{% extends 'base.html' %}`:**
    *   บอกว่าไฟล์นี้ extends (สืบทอด) มาจาก `base.html` ซึ่งหมายความว่าจะใช้โครงสร้าง HTML พื้นฐานจาก `base.html`
*   **`{% block title %}{% endblock %}`:**
    *   กำหนด title ของหน้าเว็บเป็น "Home - Liverpool FC"
*   **`{% block content %}{% endblock %}`:**
    *   ส่วนนี้เป็นเนื้อหาเฉพาะของหน้าแรก
    *   แสดงภาพต้อนรับ (Welcome To Anfield Stadium)
    *   แสดงส่วน "Memorable Things" พร้อมรูปภาพและคำอธิบายเหตุการณ์สำคัญต่างๆ แต่ละเหตุการณ์มีลิงก์ไปยังวิดีโอ YouTube ที่เกี่ยวข้อง
    *   แสดงส่วน "Liverpool FC Squad" พร้อมรูปภาพและชื่อผู้เล่นแต่ละคน

### `dashboard.html`

ไฟล์นี้เป็น template สำหรับแดชบอร์ดของผู้ใช้ (ต้องมีโค้ด Flask เพิ่มเติมเพื่อจัดการระบบ login และการเข้าถึง dashboard) ประกอบด้วย:

*   **`{% extends 'base.html' %}`:**
    *   บอกว่าไฟล์นี้ extends มาจาก `base.html`
*   **`{% block title %}{% endblock %}`:**
    *   กำหนด title ของหน้าเว็บเป็น "Dashboard - Liverpool FC"
*   **`{% block content %}{% endblock %}`:**
    *   แสดงภาพต้อนรับในแดชบอร์ด

## วิธีการรันโปรเจ็กต์ (How to Run the Project)

**ข้อควรทราบ: ไฟล์ HTML เหล่านี้เป็นเพียงส่วนหน้าบ้าน (frontend) ของเว็บไซต์ คุณต้องมีโค้ด Python และ Flask เพื่อสร้างส่วนหลังบ้าน (backend) และทำให้เว็บไซต์ทำงานได้อย่างสมบูรณ์**

1.  **ติดตั้ง Python และ Flask:**

    *   ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้ง Python แล้ว (แนะนำ Python 3.6 ขึ้นไป)
    *   ติดตั้ง Flask โดยใช้ pip:

        ```
        pip install flask
        ```

    *   ติดตั้ง Flask-Login (สำหรับระบบยืนยันตัวตน):

        ```
        pip install flask-login
        ```

    *   ติดตั้ง Werkzeug (สำหรับ hashing password):

        ```
        pip install Werkzeug
        ```

2.  **สร้างไฟล์ `app.py`:**

    *   สร้างไฟล์ `app.py` ใน directory เดียวกับโฟลเดอร์ `templates` และ `static`
    *   ใส่โค้ด Flask app ลงใน `app.py` (ตัวอย่างโค้ดด้านล่าง)

3.  **สร้างโฟลเดอร์ `templates` และ `static`:**

    *   สร้างโฟลเดอร์ `templates` และ `static` ใน directory เดียวกับ `app.py`
    *   ย้ายไฟล์ HTML (`base.html`, `index.html`, `dashboard.html`) ไปไว้ในโฟลเดอร์ `templates`
    *   สร้างโฟลเดอร์ `css` และ `images` ในโฟลเดอร์ `static`
    *   สร้างไฟล์ `style.css` ในโฟลเดอร์ `static/css` (คุณต้องเขียน CSS code เอง)
    *   ใส่รูปภาพทั้งหมดที่ใช้ในเว็บไซต์ลงในโฟลเดอร์ `static/images`

4.  **โค้ดตัวอย่าง `app.py`:**

    ```
    from flask import Flask, render_template, url_for, request, redirect
    from flask_login import LoginManager, UserMixin, login_user, logout_user, login_required, current_user
    from werkzeug.security import generate_password_hash, check_password_hash

    app = Flask(__name__)
    app.config['SECRET_KEY'] = 'your_secret_key'  # เปลี่ยนเป็นคีย์ที่ปลอดภัยกว่านี้
    # app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///site.db'  # ถ้าใช้ SQLite
    # db = SQLAlchemy(app)
    login_manager = LoginManager()
    login_manager.init_app(app)
    login_manager.login_view = 'login'

    # ตัวอย่างคลาส User (อาจต้องปรับเปลี่ยนตามโครงสร้างฐานข้อมูลของคุณ)
    class User(UserMixin):
        def __init__(self, id):
            self.id = id

        # def __init__(self, id, username, password): # ถ้ามี username/password
        #     self.id = id
        #     self.username = username
        #     self.password = password

    # โหลด User จาก ID (จำเป็นสำหรับ Flask-Login)
    @login_manager.user_loader
    def load_user(user_id):
        return User(user_id)
        # **สำคัญ:** โหลด user จากฐานข้อมูลจริง
        # user = User.query.get(int(user_id)) # ถ้าใช้ SQLAlchemy
        # return user

    @app.route('/')
    def home():
        return render_template('index.html')

    @app.route('/dashboard')
    @login_required
    def dashboard():
        return render_template('dashboard.html')

    @app.route('/login', methods=['GET', 'POST'])
    def login():
        if request.method == 'POST':
            # ตรวจสอบข้อมูลล็อกอิน (ตัวอย่าง)
            username = request.form['username']
            password = request.form['password']
            # **สำคัญ:** ตรวจสอบ username/password จากฐานข้อมูลจริง
            # user = User.query.filter_by(username=username).first() # ถ้าใช้ SQLAlchemy
            # if user and check_password_hash(user.password, password):
            #     login_user(user)
            #     return redirect(url_for('dashboard'))
            # ตัวอย่าง (สมมติว่า user ID คือ username):
            user = User(username)  # สร้าง User object จาก username
            login_user(user)
            return redirect(url_for('dashboard'))
        return render_template('login.html') # คุณต้องสร้างไฟล์ login.html

    @app.route('/logout')
    @login_required
    def logout():
        logout_user()
        return redirect(url_for('home'))

    @app.route('/register', methods=['GET', 'POST'])
    def register():
        if request.method == 'POST':
            # ดำเนินการลงทะเบียน (ตัวอย่าง)
            username = request.form['username']
            password = request.form['password']
            # **สำคัญ:** บันทึก username/password ลงในฐานข้อมูลอย่างปลอดภัย (hash password)
            # hashed_password = generate_password_hash(password, method='sha256')
            # new_user = User(username=username, password=hashed_password)
            # db.session.add(new_user)
            # db.session.commit()
            return redirect(url_for('login'))
        return render_template('register.html') # คุณต้องสร้างไฟล์ register.html

    if __name__ == '__main__':
        app.run(debug=True)
    ```

5.  **สร้างไฟล์ `login.html` และ `register.html`:**

    *   คุณต้องสร้างไฟล์ `login.html` และ `register.html` ในโฟลเดอร์ `templates` เพื่อให้ระบบ login และ register ทำงานได้อย่างถูกต้อง
    *   ตัวอย่างโค้ด `login.html`:

        ```
        {% extends 'base.html' %}

        {% block content %}
        <h2>Login</h2>
        <form method="POST" action="/login">
            <label for="username">Username:</label><br>
            <input type="text" id="username" name="username"><br><br>
            <label for="password">Password:</label><br>
            <input type="password" id="password" name="password"><br><br>
            <input type="submit" value="Login">
        </form>
        {% endblock %}
        ```

    *   ตัวอย่างโค้ด `register.html`:

        ```
        {% extends 'base.html' %}

        {% block content %}
        <h2>Register</h2>
        <form method="POST" action="/register">
            <label for="username">Username:</label><br>
            <input type="text" id="username" name="username"><br><br>
            <label for="password">Password:</label><br>
            <input type="password" id="password" name="password"><br><br>
            <input type="submit" value="Register">
        </form>
        {% endblock %}
        ```

6.  **รันแอปพลิเคชัน:**

    *   เปิด terminal หรือ command prompt
    *   cd ไปยัง directory ที่มีไฟล์ `app.py`
    *   รันคำสั่ง:

        ```
        python app.py
        ```

7.  **เข้าถึงเว็บไซต์:**

    *   เปิด web browser และไปที่ `http://127.0.0.1:5000/`
    *   คุณควรจะเห็นหน้าแรกของเว็บไซต์ Liverpool FC

