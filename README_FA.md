# 🚀 آموزش کامل اتصال به Vast.ai با VS Code (۰ تا ۱۰۰)

این راهنما همه مراحل اتصال به سرور GPU در Vast.ai و استفاده از آن در **VS Code** را توضیح می‌دهد.  

---

## 📌 فهرست مطالب
1. معرفی  
2. ساخت ماشین در Vast.ai  
3. آماده‌سازی سیستم لوکال  
4. ساخت کلید SSH  
5. اضافه کردن کلید به Vast.ai  
6. تست اتصال SSH  
7. تنظیم فایل Config  
8. اتصال با VS Code  
9. نصب پایتون و Jupyter  
10. اجرای Jupyter با Port Forwarding  
11. مدیریت ماشین Vast.ai  
12. چک‌لیست سریع  

---

## 🔹 مرحله ۱: ساخت ماشین در Vast.ai
1. ورود به [vast.ai](https://vast.ai)  
2. ثبت‌نام / ورود  
3. ایجاد ماشین (**Create Instance**)  
4. انتخاب GPU، CPU، RAM، دیسک (مثلاً RTX 3060 Ti)  
5. کلیک روی **Rent**  
6. مشاهده ماشین در بخش **Instances**  

---

## 🔹 مرحله ۲: آماده‌سازی سیستم لوکال
- نصب [VS Code](https://code.visualstudio.com/)  
- نصب [Git Bash](https://git-scm.com/download/win) (برای دستورات SSH)  
- نصب افزونه‌های VS Code:  
  - **Remote - SSH**  
  - **Jupyter** (اختیاری)  

---

## 🔹 مرحله ۳: ساخت کلید SSH
در Git Bash اجرا کنید:
```bash
ssh-keygen -t rsa -b 2048 -C "afsha@mahdi"
```

کلیدها ساخته می‌شوند:  
- `id_rsa` (خصوصی)  
- `id_rsa.pub` (عمومی)  

مشاهده کلید عمومی:
```bash
cat ~/.ssh/id_rsa.pub
```

---

## 🔹 مرحله ۴: اضافه کردن کلید به Vast.ai
1. Vast.ai → **Account → SSH Keys**  
2. کلیک روی **Add Key**  
3. پیست‌کردن متن کلید عمومی  
4. ذخیره  

---

## 🔹 مرحله ۵: تست اتصال با SSH
دستور SSH از پنل Vast.ai:
```bash
ssh -p 28305 root@121.122.125.126
```

اولین بار:  
```
yes
```

تست GPU:
```bash
nvidia-smi
```

---

## 🔹 مرحله ۶: فایل SSH Config
📂 مسیر:  
```
C:\Users\afsha\.ssh\config
```

محتوا:
```ssh-config
Host vast
    HostName 121.122.125.116
    User root
    Port 28305
    IdentityFile C:/Users/afsha/.ssh/id_rsa
    LocalForward 8080 localhost:8080
```

---

## 🔹 مرحله ۷: اتصال با VS Code
1. VS Code → `Ctrl+Shift+P`  
2. انتخاب **Remote-SSH: Connect to Host**  
3. انتخاب `vast`  
4. VS Code به سرور وصل می‌شود ✅  

---

## 🔹 مرحله ۸: نصب پایتون و Jupyter
```bash
apt update && apt install -y python3-pip
pip install torch torchvision torchaudio
pip install jupyterlab
```

---

## 🔹 مرحله ۹: اجرای Jupyter
```bash
jupyter lab --no-browser --port=8080
```

سپس در مرورگر:
```
http://localhost:8080
```

---

## 🔹 مرحله ۱۰: مدیریت ماشین Vast.ai
- بعد از کار → ماشین را **Stop** یا **Destroy** کنید  
- هزینه بر اساس ساعت محاسبه می‌شود  

---

## ✅ چک‌لیست سریع
```bash
ssh-keygen -t rsa -b 2048 -C "afsha@mahdi"
cat ~/.ssh/id_rsa.pub   # اضافه به Vast.ai

ssh -p 28305 root@121.122.125.126
nvidia-smi   # تست GPU

# Config برای VS Code
Host vast
    HostName 122.122.125.126
    User root
    Port 28302
    IdentityFile C:/Users/afsha/.ssh/id_rsa
    LocalForward 8080 localhost:8080

# نصب محیط
apt update && apt install -y python3-pip
pip install torch torchvision torchaudio
pip install jupyterlab
jupyter lab --no-browser --port=8080
```