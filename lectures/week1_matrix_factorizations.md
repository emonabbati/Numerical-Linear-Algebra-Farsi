# هفتهٔ ۱ — تفکیک‌های ماتریسی (Matrix Factorizations)

**هدف‌های جلسه**
- فهم مفهوم تفکیک LU و شرایط وجود آن.  
- مرور QR و نقش آن در حل مسائل کمترین مربعات.  
- آشنایی مقدماتی با SVD و کاربردهای آن.

---

## محتوای جلسه

### 1. مقدمه و انگیزه
در بسیاری از مسائل محاسباتی، به‌جای کار مستقیم روی ماتریس \(A\)، آن را به حاصل‌ضرب ماتریس‌های ساده‌تر فاکتورگیری می‌کنیم. اینکار هم محاسبات را سریع‌تر می‌کند و هم پایداری عددی را بهبود می‌دهد.

### 2. تفکیک LU (LU Decomposition)
فرض کنید \(A\) ماتریسی مربع و غیرتک‌ر‌دی باشد. اگر بتوانیم \(A\) را به صورت
$$
A = LU
$$
بنویسیم که در آن \(L\) ماتریس مثلثی پایین با قطرهای یک (واحد) و \(U\) ماتریس مثلثی بالا است، آنگاه حل دستگاه \(Ax=b\) به دو مرحلهٔ ساده تبدیل می‌شود:
1. حل \(Ly=b\) (پیش‌خلافش یا forward substitution)
2. حل \(Ux=y\) (back substitution)

**شرط وجود:** برای وجود تفکیک بدون جابه‌جایی سطرها (pivoting) عامل‌های سربرگ باید غیرصفر باشند. در حالت کلی نیاز به **Partial Pivoting** داریم.

برای توضیح بیشتر به واژه‌نامه مراجعه کنید: [LU Decomposition](../glossary.md#lu-decomposition).

**مثال (نوشتاری):**
اگر
$$
A=\begin{pmatrix} 2 & 3 \\ 4 & 7 \end{pmatrix},
$$
می‌خواهیم \(L\) و \(U\) را بیابیم. (جزئیات محاسبه در کلاس تشریح می‌شود.)

---

### 3. معیارهای عددی: Condition Number
شرط اعداد یا condition number یک ماتریس \(A\) را معمولاً با
$$
\kappa(A) = \|A\|\,\|A^{-1}\|
$$
تعریف می‌کنیم (برای نمونه با نورم ۲). مقدار بزرگ \(\kappa(A)\) به معنای حساسیت بالا نسبت به خطاهای ورودی است.

برای تعاریف و مثال‌ها به: [Condition Number](../glossary.md#condition-number).

---

### 4. QR و مسائل کمترین مربعات
برای حل مسئلهٔ کمترین مربعات
$$
\min_x \|Ax-b\|_2,
$$
یکی از روش‌ها تفکیک **QR** است که \(A=QR\) (با \(Q\) ماتریس اورتونورمال و \(R\) مثلثی بالا). سپس مسئله معادل حل \(Rx = Q^T b\) می‌شود.

---

### 5. SVD — معرفی کوتاه
تفکیک مقدار منفرد (SVD) برای هر ماتریس \(A \in \mathbb{R}^{m\times n}\) وجود دارد:
$$
A = U \Sigma V^T,
$$
که در آن \(U\) و \(V\) ماتریس‌های اورتونورمال و \(\Sigma\) ماتریس قطری با مقادیر منفرد است. SVD کاربردهای گسترده‌ای در فشرده‌سازی، کاهش ابعاد (PCA) و حل مسائل کمینه مربعات مرتبه ضعیف دارد.

برای مطالعهٔ عمیق‌تر به: [SVD (Singular Value Decomposition)](../glossary.md#svd-singular-value-decomposition).

---

## نمونهٔ کد (Python — NumPy)
```python
import numpy as np
A = np.array([[2.0, 3.0],
              [4.0, 7.0]])
# QR:
Q, R = np.linalg.qr(A)
print("Q:\n", Q)
print("R:\n", R)
# SVD:
U, s, VT = np.linalg.svd(A, full_matrices=False)
print("Sigma:", s)
```

---

## 🔁 پیوند داخلی به واژه‌نامه
برای توضیحات سریع و پیوند به تعاریف:
- [LU Decomposition](../glossary.md#lu-decomposition)  
- [Condition Number](../glossary.md#condition-number)  
- [SVD](../glossary.md#svd-singular-value-decomposition)

---

## ### Interactive Exercises on MyOpenMath
برای مهارت‌آموزی تعاملی، حل تمرین‌ها در MyOpenMath انجام شود:

- [تمرین‌های تعاملی: LU Decomposition — MyOpenMath](https://www.myopenmath.com/sets/lu-decomposition-example)  
- [تمرین نمونه: QR و Least Squares — MyOpenMath](https://www.myopenmath.com/sets/qr-least-squares)

(لینک‌ها قابل جایگزینی با لینک‌های واقعی کلاس شما هستند.)

---

## ### Supplementary Video
ویدیوی مرتبط (برای مشاهده روی تصویر کلیک کنید):

[![تفکیک LU — نمونه ویدیو](https://img.youtube.com/vi/VIDEO_ID_1/0.jpg)](https://www.youtube.com/watch?v=VIDEO_ID_1)

> اگر فایل ویدیویی محلی دارید، می‌توانید آن را در پوشهٔ `videos/` بارگذاری کرده و لینک مستقیم بدهید:
> - دانلود ویدیو: `videos/week1_lu_intro.mp4`

---

## منابع برای مطالعهٔ بیشتر
- فصل‌های ابتدایی مربوط به تفکیک‌ها در هر کتاب جبر خطی عددی استاندارد (به `resources/textbooks.md` مراجعه کنید).  
- مثال‌ها و تمرین‌های عملی در `homework/hw1_intro_to_factorizations.md`.

---

### تمرین (پیش‌مطالعه برای جلسهٔ بعد)
1. با دستی برای یک ماتریس \(3\times 3\) تفکیک LU را محاسبه کنید.  
2. کد Python بنویسید که برای یک ماتریس تصادفی \(A\) تفکیک QR را محاسبه کرده و بررسی کنید \(Q^T Q = I\) چقدر دقیق برقرار است.

> فایل‌های بیشتر در پوشهٔ `lectures/` موجود است. برای هر سؤال یا گزارش اشکال، لطفاً Issue باز کنید یا به ایمیل مدرس پیام دهید.
