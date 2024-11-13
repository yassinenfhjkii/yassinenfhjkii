<!DOCTYPE html>
<html lang="ar">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>صفحة تسجيل الدخول</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
    <style>
        body {
  font-family: 'Roboto', sans-serif;
    display: flex;
    align-items: center;
    justify-content: center;
    height: 100vh;
    margin: 0;
    background: url('mohamed-nohassi-2iUrK025cec-unsplash.jpg') no-repeat center center fixed;
    background-size: cover;
}

.login-container, .signup-container, .reset-password-container {
    background-color: rgba(255, 255, 255, 0.9); /* جعل الخلفية شبه شفافة */
    padding: 2rem;
    width: 300px;
    box-shadow: 0 8px 16px rgba(0, 0, 0, 0.3);
    border-radius: 8px;
    border: 2px solid #ACB6E5;
    text-align: center;
}

       
        .login-container, .signup-container, .reset-password-container {
    background-color: rgba(255, 255, 255, 0.8); /* جعل الخلفية شبه شفافة */
    padding: 2rem;
    width: 300px;
    box-shadow: 0 10px 20px rgba(0, 0, 0, 0.3), 0 6px 6px rgba(0, 0, 0, 0.1); /* تأثير 3D */
    border-radius: 12px; /* زوايا أكثر انحناءً */
    border: 2px solid rgba(172, 182, 229, 0.7); /* إطار شفاف قليلاً */
    text-align: center;
}

        .input-container {
            display: flex;
            align-items: center;
            border: 1px solid #ddd;
            border-radius: 4px;
            padding: 0.5rem;
            margin: 0.5rem 0;
            background-color: #f9f9f9;
        }

        .input-container i {
            margin-right: 8px;
            color: #888;
        }

        .input-field {
            width: 100%;
            border: none;
            outline: none;
            background: none;
        }

        .submit-btn {
            width: 100%;
            padding: 0.5rem;
            background-color: #5cb85c;
            color: #fff;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            transition: background 0.3s;
        }

        .submit-btn:hover {
            background-color: #4cae4c;
        }

        .login-container p, .signup-container p, .reset-password-container p {
            margin-top: 1rem;
            color: #666;
        }

        .error-message {
            color: red;
            margin-top: 0.5rem;
        }

        .overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.5);
            display: none;
        }

        .signup-popup {
            display: none;
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background-color: #fff;
            padding: 2rem;
            width: 300px;
            box-shadow: 0 8px 16px rgba(0, 0, 0, 0.3);
            border-radius: 8px;
            border: 2px solid #ACB6E5;
            text-align: center;
        }

        .reset-password-popup {
            display: none;
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background-color: #fff;
            padding: 2rem;
            width: 300px;
            box-shadow: 0 8px 16px rgba(0, 0, 0, 0.3);
            border-radius: 8px;
            border: 2px solid #ACB6E5;
            text-align: center;
        }

    </style>
</head>
<body>
    <div class="login-container">
        <h2>تسجيل الدخول</h2>
        <div class="input-container">
            <i class="fas fa-user"></i>
            <input type="text" class="input-field" placeholder="اسم المستخدم" id="username">
        </div>
        <div class="input-container">
            <i class="fas fa-lock"></i>
            <input type="password" class="input-field" placeholder="كلمة المرور" id="password">
        </div>
        <div id="login-message" class="error-message"></div>
        <button class="submit-btn" onclick="validateLogin()">دخول</button>
        <p>ليس لديك حساب؟ <a href="#" onclick="openSignup()">إنشاء حساب</a></p>
        <p><a href="#" onclick ="openResetPassword()">نسيت كلمة المرور</a></p>
    </div>

    <div class="overlay" id="overlay" onclick="closeSignup()"></div>
    <div class="signup-popup" id="signup-popup">
        <h2>إنشاء حساب</h2>
        <div class="input-container">
            <i class="fas fa-user"></i>
            <input type="text" class="input-field" placeholder="اسم المستخدم" id="signup-username">
        </div>
        <div class="input-container">
            <i class="fas fa-envelope"></i>
            <input type="email" class="input-field" placeholder="البريد الإلكتروني" id="signup-email">
        </div>
        <div class="input-container">
            <i class="fas fa-lock"></i>
            <input type="password" class="input-field" placeholder="كلمة المرور" id="signup-password">
        </div>
        <div class="input-container">
            <i class="fas fa-lock"></i>
            <input type="password" class="input-field" placeholder="تأكيد كلمة المرور" id="signup-confirm-password">
        </div>
        <div id="signup-message" class="error-message"></div>
        <button class="submit-btn" onclick="validateSignup()">إنشاء حساب</button>
        <p>لديك حساب؟ <a href="#" onclick="closeSignup()">تسجيل الدخول</a></p>
    </div>

    <div class="overlay" id="reset-password-overlay" onclick="closeResetPassword()"></div>
    <div class="reset-password-popup" id="reset-password-popup">
        <h2>إعادة تعيين كلمة المرور</h2>
        <div class="input-container">
            <i class="fas fa-envelope"></i>
            <input type="email" class="input-field" placeholder="البريد الإلكتروني" id="reset-password-email">
        </div>
        <div id="reset-password-message" class="error-message"></div>
        <button class="submit-btn" onclick="resetPassword()">إعادة تعيين كلمة المرور</button>
        <p><a href="#" onclick="closeResetPassword()">العودة إلى تسجيل الدخول</a></p>
    </div>

    <script>
        function validateLogin() {
            const username = document.getElementById("username").value;
            const password = document.getElementById("password").value;

            if (username === "" || password === "") {
                document.getElementById("login-message").innerHTML = "يرجى ملء جميع الحقول";
                return;
            }

            // logic to validate login credentials
            // ...

            // if login is successful, redirect to dashboard
            window.location.href = "dashboard.html";
        }

        function openSignup() {
            document.getElementById("overlay").style.display = "block";
            document.getElementById("signup-popup").style.display = "block";
        }

        function closeSignup() {
            document.getElementById("overlay").style.display = "none";
            document.getElementById("signup-popup").style.display = "none";
        }

        function validateSignup() {
            const signupUsername = document.getElementById("signup-username").value;
            const signupEmail = document.getElementById("signup-email").value;
            const signupPassword = document.getElementById("signup-password").value;
            const signupConfirmPassword = document.getElementById("signup-confirm-password").value;

            if (signupUsername === "" || signupEmail === "" || signupPassword === "" || signupConfirmPassword === "") {
                document.getElementById("signup-message").innerHTML = "يرجى ملء جميع الحقول";
                return;
            }

            if (signupPassword !== signupConfirmPassword) {
                document.getElementById("signup-message").innerHTML = "كلمة المرور غير متطابقة";
                return;
            }

            // logic to validate signup credentials
            // ...

            // if signup is successful, redirect to dashboard
            window.location.href = "dashboard.html";
        }

        function openResetPassword() {
            document.getElementById("reset-password-overlay").style.display = "block";
            document.getElementById("reset-password-popup").style.display = "block";
        }

        function closeResetPassword() {
            document.getElementById("reset-password-overlay").style.display = "none";
            document.getElementById("reset-password-popup").style.display = "none";
        }

        function resetPassword() {
            const resetPasswordEmail = document.getElementById("reset-password-email").value;

            if (resetPasswordEmail === "") {
                document.getElementById("reset-password-message").innerHTML = "يرجى ملء البريد الإلكتروني";
                return;
            }

            // logic to reset password
            // ...

            // if password reset is successful, redirect to login page
            window.location.href = "login.html";
        }
    </script>
     <script src="script.js"></script>
</body>
</html>
