```css
/* Animated Liquid Background */
body {
    font-family: 'Poppins', sans-serif;
    margin: 0;
    color: white;
    background: linear-gradient(-45deg, #1b5e20, #2e7d32, #e65100, #bf360c);
    background-size: 400% 400%;
    animation: gradientBG 15s ease infinite;
    overflow-x: hidden;
    min-height: 100vh;
}

@keyframes gradientBG {
    0% { background-position: 0% 50%; }
    50% { background-position: 100% 50%; }
    100% { background-position: 0% 50%; }
}

/* Header Styles */
header { 
    padding: 80px 20px;
    text-align: center;
    background: var(--dark-glass);
    backdrop-filter: blur(15px);
    border-bottom: 5px solid var(--honey);
    box-shadow: 0 10px 30px rgba(0,0,0,0.3);
}

header h1 { 
    font-family: 'Bungee', cursive; 
    font-size: clamp(2.5rem, 10vw, 5rem); 
    margin: 0;
    color: var(--honey);
    text-shadow: 5px 5px 0 var(--brand-orange);
    letter-spacing: 2px;
    animation: titlePulse 2s infinite alternate;
}

@keyframes titlePulse {
    from { transform: scale(1); filter: drop-shadow(0 0 5px var(--honey)); }
    to { transform: scale(1.02); filter: drop-shadow(0 0 20px var(--brand-orange)); }
}

.service-banner {
    background: white;
    color: var(--brand-green);
    padding: 10px 25px;
    border-radius: 50px;
    font-weight: 900;
    display: inline-block;
    margin-top: 20px;
    box-shadow: 0 5px 15px rgba(0,0,0,0.2);
}

.container { 
    width: 100%; 
    max-width: 1200px; 
    margin: 0 auto; 
    padding: 20px; 
    box-sizing: border-box; 
}

.category-title { 
    font-family: 'Bungee', cursive;
    font-size: 2rem;
    margin: 60px 0 30px;
    text-align: center;
    position: relative;
}

.category-title::after {
    content: '';
    display: block;
    width: 80px;
    height: 4px;
    background: var(--honey);
    margin: 10px auto;
    border-radius: 2px;
}

/* Fixed CSS Grid layout */
.menu-grid { 
    display: grid; 
    grid-template-columns: repeat(auto-fill, minmax(280px, 1fr)); 
    gap: 30px; 
    width: 100%;
    box-sizing: border-box;
}

.food-card { 
    background: rgba(255, 255, 255, 0.95);
    color: #1a1a1a;
    border-radius: 30px;
    padding: 25px;
    box-shadow: 0 15px 35px rgba(0,0,0,0.2);
    transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
    border: 1px solid rgba(255,255,255,0.3);
    display: flex;
    flex-direction: column;
    justify-content: space-between;
}

.food-card:hover {
    transform: translateY(-15px) scale(1.03);
    background: white;
    box-shadow: 0 25px 50px rgba(255, 109, 0, 0.3);
}

.food-name { font-weight: 900; font-size: 1.2rem; color: var(--brand-green); }
.food-price { font-weight: 900; font-size: 1.5rem; color: var(--brand-orange); margin: 10px 0; }

.btn-add { 
    background: linear-gradient(45deg, var(--brand-green), #43a047);
    color: white; border: none; width: 100%;
    padding: 15px; border-radius: 20px; font-weight: 900; 
    cursor: pointer; transition: 0.3s;
    text-transform: uppercase; letter-spacing: 1px;
}

.btn-add:active { transform: scale(0.95); }

/* Cart Floating Button */
.cart-toggle { 
    position: fixed; bottom: 30px; right: 30px; 
    background: var(--brand-orange);
    color: white; padding: 20px 35px; border-radius: 100px;
    cursor: pointer; font-weight: 900; z-index: 2000;
    box-shadow: 0 10px 30px rgba(0,0,0,0.5);
    border: 4px solid var(--honey);
    transition: 0.3s;
}

.cart-toggle:hover { transform: scale(1.1); }

/* Side Panel (Glassmorphism) */
#cart-panel { 
    position: fixed; top: 0; right: -100%; width: 100%; max-width: 450px; height: 100%;
    background: rgba(255, 255, 255, 0.95);
    backdrop-filter: blur(10px);
    color: #1a1a1a; z-index: 3000; padding: 40px;
    transition: 0.5s cubic-bezier(0.77, 0, 0.175, 1);
    box-shadow: -10px 0 50px rgba(0,0,0,0.3);
    display: flex; flex-direction: column;
}

#cart-panel.active { right: 0; }

.cart-item {
    display: flex; justify-content: space-between; align-items: center;
    padding: 15px 0; border-bottom: 2px dashed #ddd;
    animation: fadeIn 0.5s ease;
}

@keyframes fadeIn {
    from { opacity: 0; transform: translateX(20px); }
    to { opacity: 1; transform: translateX(0); }
}

.btn-unpick {
    background: #ffebee; color: #d32f2f; border: 2px solid #d32f2f;
    padding: 8px 15px; border-radius: 12px; font-weight: 800; cursor: pointer;
}

/* Payment Modal */
#payment-modal {
    display: none; position: fixed; top: 50%; left: 50%; transform: translate(-50%, -50%);
    width: 90%; max-width: 400px; background: white; color: #1a1a1a;
    padding: 40px; border-radius: 40px; z-index: 5000; text-align: center;
    box-shadow: 0 0 100px rgba(0,0,0,0.5);
    border: 8px solid var(--brand-orange);
    animation: modalPop 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
}

@keyframes modalPop {
    from { transform: translate(-50%, -50%) scale(0.5); opacity: 0; }
    to { transform: translate(-50%, -50%) scale(1); opacity: 1; }
}

.bank-card {
    background: #f8f9fa; padding: 25px; border-radius: 25px; 
    margin: 20px 0; border: 2px dashed var(--brand-green);
}

.btn-whatsapp { 
    background: #25d366; color: white; border: none; width: 100%;
    padding: 20px; border-radius: 20px; font-weight: 900; font-size: 1.2rem;
    cursor: pointer; box-shadow: 0 10px 20px rgba(37, 211, 102, 0.3);
}

footer { 
    background: var(--dark-glass); padding: 60px 20px; text-align: center; 
    border-top: 10px solid var(--honey); 
}

/* Scrollbar */
::-webkit-scrollbar { width: 10px; }
::-webkit-scrollbar-track { background: transparent; }
::-webkit-scrollbar-thumb { background: var(--honey); border-radius: 10px; }

/* Responsive Breakpoint Mobile adjustment */
@media (max-width: 600px) {
    header h1 { 
        font-size: 2.2rem; 
    }
    #cart-panel { 
        width: 100%; 
        max-width: 100%; 
    }
    .container {
        padding: 10px; 
    }
}
