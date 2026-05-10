<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Blessed 9ra | Mobile-Ready Menu</title>
    <link href="https://fonts.googleapis.com/css2?family=Bungee&family=Poppins:wght@400;600;900&display=swap" rel="stylesheet">
    <style>
        :root {
            --brand-green: #2e7d32;
            --brand-orange: #ff6d00;
            --honey: #ffc107;
            --white: #ffffff;
        }

        /* Responsive Flowing Background */
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
            100% { transform: translateY(-20vh) rotate(360deg); opacity: 0; }
        }

        .floating-emoji {
            position: fixed; z-index: -1; font-size: 2rem; pointer-events: none;
        }

        /* Mobile-Responsive Header */
        header { 
            padding: 60px 15px; text-align: center;
            background: rgba(0, 0, 0, 0.4);
            backdrop-filter: blur(10px);
            border-bottom: 6px solid var(--honey);
        }

        header h1 { 
            font-family: 'Bungee', cursive; 
            font-size: clamp(2rem, 10vw, 4rem); 
            margin: 0; color: var(--honey);
            text-shadow: 3px 3px 0 var(--brand-orange);
        }

        .container { width: 100%; max-width: 1200px; margin: 0 auto; padding: 20px; box-sizing: border-box; }
        
        .category-title { 
            font-family: 'Bungee', cursive; font-size: clamp(1.5rem, 5vw, 2.2rem); 
            text-align: center; margin: 40px 0 20px;
        }

        /* Adaptive Grid */
        .menu-grid { 
            display: grid; 
            grid-template-columns: repeat(auto-fill, minmax(280px, 1fr)); 
            gap: 20px; 
        }

        /* Card Adjustments */
        .food-card { 
            background: rgba(255, 255, 255, 0.98); color: #1a1a1a;
            border-radius: 25px; padding: 20px; 
            box-shadow: 0 10px 20px rgba(0,0,0,0.2);
            display: flex; flex-direction: column; justify-content: space-between;
            transition: transform 0.3s ease;
        }

        .food-name { font-weight: 900; font-size: 1.2rem; color: var(--brand-green); }
        .food-price { font-weight: 900; font-size: 1.4rem; color: var(--brand-orange); margin: 10px 0; }

        .btn-add { 
            background: var(--brand-green); color: white; border: none; width: 100%;
            padding: 12px; border-radius: 15px; font-weight: 900; cursor: pointer;
        }

        /* Mobile-Friendly Cart Panel */
        .cart-toggle { 
            position: fixed; bottom: 20px; right: 20px; background: var(--brand-orange); 
            color: white; padding: 15px 25px; border-radius: 50px; 
            cursor: pointer; font-weight: 900; z-index: 2000; 
            box-shadow: 0 10px 25px rgba(0,0,0,0.4); border: 3px solid var(--honey);
            font-size: 0.9rem;
        }

        #cart-panel { 
            position: fixed; top: 0; right: -100%; width: 100%; max-width: 400px; height: 100%; 
            background: white; color: #1a1a1a; z-index: 3000; padding: 25px; 
            transition: 0.4s cubic-bezier(0.4, 0, 0.2, 1); display: flex; flex-direction: column;
            box-shadow: -5px 0 25px rgba(0,0,0,0.3);
        }
        #cart-panel.active { right: 0; }

        .cart-item {
            display: flex; justify-content: space-between; align-items: center;
            padding: 12px 0; border-bottom: 1px dashed #ccc;
        }

        .btn-unpick {
            background: #ffeded; color: #d32f2f; border: 1px solid #d32f2f;
            padding: 6px 12px; border-radius: 8px; font-weight: 800; cursor: pointer;
        }

        /* Payment Modal Responsive */
        #payment-modal {
            display: none; position: fixed; top: 50%; left: 50%; transform: translate(-50%, -50%);
            width: 90%; max-width: 380px; background: white; color: #1a1a1a;
            padding: 25px; border-radius: 30px; z-index: 5000; text-align: center;
            border: 5px solid var(--brand-orange);
        }

        .bank-info { background: #f4f4f4; padding: 15px; border-radius: 15px; margin: 15px 0; }

        .btn-whatsapp { background: #25d366; color: white; border: none; width: 100%; padding: 15px; border-radius: 12px; font-weight: 900; font-size: 1.1rem; cursor: pointer; }

        footer { background: rgba(0,0,0,0.9); padding: 40px 15px; text-align: center; border-top: 6px solid var(--honey); }

        /* Media Query for Tiny Screens */
        @media (max-width: 350px) {
            .menu-grid { grid-template-columns: 1fr; }
            #cart-panel { max-width: 100%; }
        }
    </style>
</head>
<body>

<div id="emoji-layer"></div>

<div class="cart-toggle" onclick="toggleCart()">🛒 TRAY (<span id="cart-count">0</span>)</div>

<div id="payment-modal">
    <h2 style="font-family:'Bungee';">PAYMENT</h2>
    <div class="bank-info">
        <h2 style="margin:0; color:var(--brand-orange);">5391538148</h2>
        <p style="margin:5px 0;"><b>Moniepoint</b></p>
        <p style="margin:0; font-size:0.9rem;">Name: Blessed9ra</p>
    </div>
    <button class="btn-whatsapp" onclick="sendOrder()">PROCEED TO WHATSAPP 🚀</button>
    <p onclick="closePayment()" style="margin-top:15px; cursor:pointer; text-decoration:underline;">Go Back</p>
</div>

<div id="cart-panel">
    <div style="display:flex; justify-content:space-between; align-items:center;">
        <h2 style="font-family:'Bungee'; color:var(--brand-green); margin:0;">TRAY</h2>
        <button onclick="toggleCart()" style="border:none; background:none; font-size:2rem; cursor:pointer;">&times;</button>
    </div>
    <div id="cart-items" style="flex-grow:1; overflow-y:auto; margin: 15px 0;"></div>
    <div style="border-top:4px solid var(--honey); padding-top:15px;">
        <h3 style="display:flex; justify-content:space-between; margin-bottom:15px;">TOTAL: <span>₦<span id="cart-total">0</span></span></h3>
        <button class="btn-whatsapp" style="background:var(--brand-green)" onclick="openPayment()">CHECKOUT 💳</button>
    </div>
</div>

<header>
    <h1>BLESSED 9RA</h1>
    <p style="font-weight:900; font-size:0.9rem; letter-spacing:1px; color:var(--honey);">Lagos / Ilishan-Remo Delivery</p>
</header>

<div class="container">
    <div id="menu-sections"></div>
</div>

<footer>
    <h3 style="font-family:'Bungee'; color:var(--honey); margin:0;">BLESSED 9RA</h3>
    <p style="margin:10px 0;">📞 08168543377</p>
    <p style="font-size:0.8rem; opacity:0.7;">Powered by Blessed 9ra Delicacies</p>
</footer>

<script>
    const menuData = {
        "Base Dishes 🌾": [
            {n: "White Rice 🌾", p: 400}, {n: "Jollof Rice 🌾", p: 400}, 
            {n: "Beans 🫘", p: 400}, {n: "Plantain 🌱", p: 500}
        ],
        "Swallow & Soups 🍛": [
            {n: "Fufu / Amala / Poundo", p: 400},
            {n: "Egusi / Efo Riro 🍲", p: 600}, {n: "Ewedu-Gbegiri 🍲", p: 500}
        ],
        "Proteins 🥩": [
            {n: "Beef Meat 🥩", p: 500}, {n: "Turkey 🦃", p: 3500}, {n: "Chicken 🐓", p: 2000},
            {n: "Ponmo 🍖", p: 500}, {n: "Egg 🥚", p: 400}, {n: "Fish 🐠", p: 2000}
        ],
        "Specials 🔥": [
            {n: "Suya Rice w/ Beef", p: 4500}, {n: "Yam & Egg Sauce", p: 5500}, 
            {n: "Fried Egg & Plantain", p: 7500}, {n: "Pepper Soup 🥣", p: 7500},
            {n: "Takeaway Plate 🍱", p: 300}
        ]
    };

    let tray = [];
    const phone = "08168543377";

    function spawnIcons() {
        const icons = ['🍲', '🍗', '🌾', '🔥'];
        const layer = document.getElementById('emoji-layer');
        setInterval(() => {
            if(window.innerWidth < 600) return; // Disable on small mobile for performance
            const e = document.createElement('div');
            e.className = 'floating-emoji';
            e.innerText = icons[Math.floor(Math.random()*icons.length)];
            e.style.left = Math.random() * 90 + 'vw';
            e.style.animation = `floatUp ${6 + Math.random()*4}s linear forwards`;
            layer.appendChild(e);
            setTimeout(() => e.remove(), 8000);
        }, 3000);
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
    }

    function unpick(id) {
        tray = tray.filter(item => item.id !== id);
        updateTrayUI();
    }

    function updateTrayUI() {
        const list = document.getElementById('cart-items');
        document.getElementById('cart-count').innerText = tray.length;
        let sum = 0; list.innerHTML = "";
        
        tray.forEach(i => {
            sum += i.price;
            list.innerHTML += `
                <div class="cart-item">
                    <div style="font-size:0.9rem;"><b>${i.name}</b><br>₦${i.price}</div>
                    <button class="btn-unpick" onclick="unpick(${i.id})">REMOVE</button>
                </div>`;
        });
        document.getElementById('cart-total').innerText = sum.toLocaleString();
    }

    function toggleCart() { document.getElementById('cart-panel').classList.toggle('active'); }
    function openPayment() { document.getElementById('payment-modal').style.display = 'block'; }
    function closePayment() { document.getElementById('payment-modal').style.display = 'none'; }

    function sendOrder() {
        let msg = "Blessed 9ra Order:%0A";
        tray.forEach(i => msg += `- ${i.name}%0A`);
        msg += `%0A*TOTAL: ₦${document.getElementById('cart-total').innerText}*%0A%0A*Moniepoint Paid*`;
        window.open(`https://wa.me/234${phone.substring(1)}?text=${msg}`, '_blank');
    }

    window.onload = init;
</script>
</body>
</html>
