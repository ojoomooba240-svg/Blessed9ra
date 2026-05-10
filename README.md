<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Blessed 9ra | The Live Experience</title>
    <link href="https://fonts.googleapis.com/css2?family=Bungee&family=Poppins:wght@400;600;900&display=swap" rel="stylesheet">
    <style>
        :root {
            --brand-green: #2e7d32;
            --brand-orange: #ff6d00;
            --honey: #ffc107;
            --white: #ffffff;
        }

        /* Animated Energy Background */
        @keyframes flow {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }

        body {
            font-family: 'Poppins', sans-serif;
            margin: 0;
            background: linear-gradient(-45deg, #1b5e20, #2e7d32, #ff6d00, #e65100);
            background-size: 400% 400%;
            animation: flow 15s ease infinite;
            color: white;
            overflow-x: hidden;
        }

        /* Floating Food Icons */
        @keyframes floatUp {
            0% { transform: translateY(110vh) rotate(0deg); opacity: 0; }
            10% { opacity: 0.5; }
            90% { opacity: 0.5; }
            100% { transform: translateY(-20vh) rotate(360deg); opacity: 0; }
        }

        .floating-emoji {
            position: fixed; z-index: -1; font-size: 2.5rem; pointer-events: none;
        }

        header { 
            padding: 80px 20px; text-align: center;
            background: rgba(0, 0, 0, 0.4);
            backdrop-filter: blur(12px);
            border-bottom: 8px solid var(--honey);
        }

        header h1 { 
            font-family: 'Bungee', cursive; font-size: clamp(2.5rem, 8vw, 4.5rem); 
            margin: 0; color: var(--honey);
            text-shadow: 4px 4px 0 var(--brand-orange);
        }

        .container { max-width: 1200px; margin: 0 auto; padding: 40px 20px; }
        
        .category-title { 
            font-family: 'Bungee', cursive; font-size: 2.2rem; text-align: center;
            margin: 50px 0 25px; text-shadow: 2px 2px 10px rgba(0,0,0,0.3);
        }

        .menu-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 25px; }
        
        .food-card { 
            background: rgba(255, 255, 255, 0.98); color: #1a1a1a;
            border-radius: 35px; padding: 25px; 
            box-shadow: 0 15px 30px rgba(0,0,0,0.2);
            transition: 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            display: flex; flex-direction: column; justify-content: space-between;
        }

        .food-card:hover { transform: scale(1.05) translateY(-10px); }

        .food-name { font-weight: 900; font-size: 1.3rem; color: var(--brand-green); margin-bottom: 5px; }
        .food-price { font-weight: 900; font-size: 1.5rem; color: var(--brand-orange); margin-bottom: 15px; }

        .btn-add { 
            background: var(--brand-green); color: white; border: none; width: 100%;
            padding: 14px; border-radius: 18px; font-weight: 900; cursor: pointer;
        }

        /* Cart Toggle Button */
        .cart-toggle { 
            position: fixed; bottom: 30px; right: 30px; background: var(--brand-orange); 
            color: white; padding: 18px 35px; border-radius: 100px; 
            cursor: pointer; font-weight: 900; z-index: 2000; 
            box-shadow: 0 10px 30px rgba(0,0,0,0.3); border: 4px solid var(--honey);
        }

        /* Side Panel */
        #cart-panel { 
            position: fixed; top: 0; right: -450px; width: 400px; height: 100%; 
            background: white; color: #1a1a1a; z-index: 3000; padding: 35px; 
            transition: 0.5s; display: flex; flex-direction: column;
            box-shadow: -10px 0 50px rgba(0,0,0,0.3);
        }
        #cart-panel.active { right: 0; }

        .cart-item {
            display: flex; justify-content: space-between; align-items: center;
            padding: 15px 0; border-bottom: 2px dashed #ddd;
        }

        /* NEW UNPICK BUTTON STYLE */
        .btn-unpick {
            background: #ffeded; color: #d32f2f; border: 1px solid #d32f2f;
            padding: 5px 10px; border-radius: 10px; font-weight: 800; cursor: pointer; font-size: 0.8rem;
        }
        .btn-unpick:hover { background: #d32f2f; color: white; }

        /* Payment Modal */
        #payment-modal {
            display: none; position: fixed; top: 50%; left: 50%; transform: translate(-50%, -50%);
            width: 90%; max-width: 420px; background: white; color: #1a1a1a;
            padding: 35px; border-radius: 40px; z-index: 5000; text-align: center;
            border: 6px solid var(--brand-orange); box-shadow: 0 0 100px rgba(0,0,0,0.6);
        }

        .bank-info { background: #f9f9f9; padding: 20px; border-radius: 20px; margin: 15px 0; border: 2px solid #eee; }

        .btn-whatsapp { background: #25d366; color: white; border: none; width: 100%; padding: 18px; border-radius: 18px; font-weight: 900; font-size: 1.2rem; cursor: pointer; }

        footer { background: rgba(0,0,0,0.85); padding: 60px 20px; text-align: center; border-top: 8px solid var(--honey); }
    </style>
</head>
<body>

<div id="emoji-layer"></div>

<div class="cart-toggle" onclick="toggleCart()">🛒 TRAY (<span id="cart-count">0</span>)</div>

<div id="payment-modal">
    <h2 style="font-family:'Bungee'; color:var(--brand-green);">SECURE PAYMENT</h2>
    <div class="bank-info">
        <h1 style="margin:0; color:var(--brand-orange); letter-spacing:1px;">5391538148</h1>
        <p style="margin:5px 0; font-weight:900;">Moniepoint</p>
        <p style="margin:0;">Account Name: <b>Blessed9ra</b></p>
    </div>
    <p style="font-size:0.9rem;">Once paid, click below to send your order and receipt to our WhatsApp!</p>
    <button class="btn-whatsapp" onclick="sendOrder()">SEND ORDER & RECEIPT 🚀</button>
    <p onclick="closePayment()" style="margin-top:20px; cursor:pointer; text-decoration:underline;">Go Back</p>
</div>

<div id="cart-panel">
    <div style="display:flex; justify-content:space-between; align-items:center;">
        <h2 style="font-family:'Bungee'; color:var(--brand-green);">YOUR TRAY</h2>
        <button onclick="toggleCart()" style="border:none; background:none; font-size:2.5rem; cursor:pointer;">&times;</button>
    </div>
    <div id="cart-items" style="flex-grow:1; overflow-y:auto; margin: 20px 0;"></div>
    <div style="border-top:5px solid var(--honey); padding-top:20px;">
        <h3 style="display:flex; justify-content:space-between; font-size:1.6rem; margin-bottom:15px;">TOTAL: <span>₦<span id="cart-total">0</span></span></h3>
        <button class="btn-whatsapp" style="background:var(--brand-green)" onclick="openPayment()">PROCEED TO CHECKOUT 💳</button>
    </div>
</div>

<header>
    <h1>BLESSED 9RA</h1>
    <p style="font-weight:900; letter-spacing:2px; color:var(--honey);">AUTHENTIC NIGERIAN DELICACIES</p>
</header>

<div class="container">
    <div id="menu-sections"></div>
</div>

<footer>
    <h2 style="font-family:'Bungee'; color:var(--honey);">BLESSED 9RA</h2>
    <p style="font-size: 1.4rem; font-weight: 800; margin: 10px 0;">📞 Contact: 08168543377</p>
    <p>📍 Ilishan-Remo, Ogun State</p>
</footer>

<script>
    const menuData = {
        "Base Dishes 🌾": [
            {n: "White Rice (Scoop) 🌾", p: 400}, {n: "Jollof Rice (Scoop) 🌾", p: 400}, 
            {n: "Beans (Scoop) 🫘", p: 400}, {n: "Plantain 🌱", p: 500}
        ],
        "Swallow & Soups 🍛": [
            {n: "Fufu / Amala / Poundo 🍛", p: 400},
            {n: "Egusi Soup (Scoop) 🍲", p: 600}, {n: "Efo Riro (Scoop) 🍲", p: 600}, {n: "Ewedu-Gbegiri 🍲", p: 500}
        ],
        "Proteins 🥩": [
            {n: "Beef Meat 🥩", p: 500}, {n: "Turkey 🦃", p: 3500}, {n: "Chicken 🐓", p: 2000},
            {n: "Ponmo 🍖", p: 500}, {n: "Egg 🥚", p: 400}, {n: "Large Fish 🐠", p: 2000}, {n: "Medium Fish 🐠", p: 1500}
        ],
        "Elite Specials 🔥": [
            {n: "Suya Rice w/ Shredded Beef", p: 4500}, 
            {n: "Yam & Fish Sauce", p: 5500}, 
            {n: "Yam & Egg Sauce", p: 5500},
            {n: "Fried Egg & Plantain", p: 7500},
            {n: "Premium Pepper Soup 🥣", p: 7500},
            {n: "Takeaway Plate 🍱", p: 300}
        ]
    };

    let tray = [];
    const phone = "08168543377";

    function spawnIcons() {
        const icons = ['🍲', '🍗', '🌾', '🔥', '🥘'];
        const layer = document.getElementById('emoji-layer');
        setInterval(() => {
            const e = document.createElement('div');
            e.className = 'floating-emoji';
            e.innerText = icons[Math.floor(Math.random()*icons.length)];
            e.style.left = Math.random() * 100 + 'vw';
            e.style.animation = `floatUp ${5 + Math.random()*5}s linear forwards`;
            layer.appendChild(e);
            setTimeout(() => e.remove(), 9000);
        }, 2000);
    }

    function init() {
        const target = document.getElementById('menu-sections');
        for (let cat in menuData) {
            let html = `<h2 class="category-title">${cat}</h2><div class="menu-grid">`;
            menuData[cat].forEach(item => {
                html += `
                    <div class="food-card">
                        <div>
                            <div class="food-name">${item.n}</div>
                            <div class="food-price">₦${item.p.toLocaleString()}</div>
                        </div>
                        <button class="btn-add" onclick="addToTray('${item.n}', ${item.p})">ADD +</button>
                    </div>`;
            });
            html += `</div>`;
            target.innerHTML += html;
        }
        spawnIcons();
    }

    function addToTray(name, price) {
        tray.push({ name, price, id: Date.now() });
        updateTrayUI();
        const count = document.getElementById('cart-count');
        count.parentElement.style.transform = "scale(1.2)";
        setTimeout(() => count.parentElement.style.transform = "scale(1)", 200);
    }

    /* THE UNPICK LOGIC */
    function unpick(id) {
        tray = tray.filter(item => item.id !== id);
        updateTrayUI();
    }

    function updateTrayUI() {
        const list = document.getElementById('cart-items');
        document.getElementById('cart-count').innerText = tray.length;
        let sum = 0; list.innerHTML = "";
        
        if (tray.length === 0) {
            list.innerHTML = "<p style='text-align:center; color:#888; margin-top:40px;'>Tray is empty!</p>";
        } else {
            tray.forEach(i => {
                sum += i.price;
                list.innerHTML += `
                    <div class="cart-item">
                        <div>
                            <div style="font-weight:900;">${i.name}</div>
                            <div style="color:var(--brand-orange);">₦${i.price}</div>
                        </div>
                        <button class="btn-unpick" onclick="unpick(${i.id})">UNPICK</button>
                    </div>`;
            });
        }
        document.getElementById('cart-total').innerText = sum.toLocaleString();
    }

    function toggleCart() { document.getElementById('cart-panel').classList.toggle('active'); }
    function openPayment() { document.getElementById('payment-modal').style.display = 'block'; }
    function closePayment() { document.getElementById('payment-modal').style.display = 'none'; }

    function sendOrder() {
        if (tray.length === 0) return alert("Your tray is empty!");
        let msg = "Hello Blessed 9ra! I just paid to your Moniepoint. Here is my order:%0A%0A";
        tray.forEach(i => msg += `- ${i.name}%0A`);
        msg += `%0A*GRAND TOTAL: ₦${document.getElementById('cart-total').innerText}*%0A%0A*Paid to Moniepoint (Blessed9ra)*`;
        window.open(`https://wa.me/234${phone.substring(1)}?text=${msg}`, '_blank');
    }

    window.onload = init;
</script>
</body>
</html>
