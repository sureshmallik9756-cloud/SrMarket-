# SrMarket-
welcome to my your soping platform It is one of the most trusted places in India.
<!DOCTYPE html>
<html lang="hi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MallikMart - ऑनलाइन शॉपिंग</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Inter', system-ui, -apple-system, sans-serif;
        }

        body {
            background-color: #f4f5f7;
            color: #1f2a3e;
        }

        :root {
            --mm-blue: #1a5cff;
            --mm-dark-blue: #0a3bb8;
            --mm-light-blue: #eef3ff;
            --mm-gold: #ffb700;
            --mm-border: #e2e5e9;
        }

        .top-bar {
            background-color: white;
            box-shadow: 0 1px 4px rgba(0,0,0,0.05);
            position: sticky;
            top: 0;
            z-index: 100;
        }

        .header-main {
            max-width: 1200px;
            margin: auto;
            padding: 12px 20px;
            display: flex;
            flex-wrap: wrap;
            align-items: center;
            justify-content: space-between;
            gap: 15px;
        }

        .logo h1 {
            color: var(--mm-blue);
            font-size: 24px;
            font-weight: 700;
        }

        .search-bar {
            flex: 1;
            min-width: 250px;
            display: flex;
        }

        .search-bar input {
            width: 100%;
            padding: 10px 16px;
            border: 1px solid var(--mm-border);
            border-radius: 20px 0 0 20px;
            outline: none;
        }

        .search-bar button {
            background-color: var(--mm-blue);
            border: none;
            padding: 0 15px;
            border-radius: 0 20px 20px 0;
            cursor: pointer;
            color: white;
        }

        .nav-icons {
            display: flex;
            gap: 15px;
            align-items: center;
        }

        .cart-icon {
            background-color: var(--mm-light-blue);
            padding: 8px 12px;
            border-radius: 20px;
            color: var(--mm-blue);
            cursor: pointer;
            font-weight: 600;
        }

        .category-bar {
            background: white;
            border-top: 1px solid var(--mm-border);
            padding: 10px 20px;
            overflow-x: auto;
            white-space: nowrap;
            text-align: center;
        }

        .category-list span {
            margin: 0 10px;
            font-size: 14px;
            cursor: pointer;
            font-weight: 500;
        }

        .container {
            max-width: 1200px;
            margin: 20px auto;
            padding: 0 15px;
        }

        .hero {
            background: linear-gradient(135deg, var(--mm-dark-blue), var(--mm-blue));
            border-radius: 15px;
            padding: 30px;
            color: white;
            text-align: center;
            margin-bottom: 30px;
        }

        .product-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(180px, 1fr));
            gap: 20px;
        }

        .product-card {
            background: white;
            border-radius: 12px;
            padding: 15px;
            text-align: center;
            border: 1px solid var(--mm-border);
            transition: 0.3s;
        }

        .product-card:hover {
            box-shadow: 0 10px 20px rgba(0,0,0,0.1);
        }

        .product-img {
            font-size: 50px;
            background: #f8f9fc;
            border-radius: 10px;
            padding: 20px 0;
            margin-bottom: 10px;
        }

        .price {
            color: var(--mm-blue);
            font-weight: 700;
            font-size: 18px;
            margin: 10px 0;
        }

        .add-btn {
            background-color: var(--mm-blue);
            color: white;
            border: none;
            padding: 8px;
            width: 100%;
            border-radius: 5px;
            cursor: pointer;
        }

        /* Cart Overlay */
        .cart-overlay {
            display: none;
            position: fixed;
            top: 0; right: 0; bottom: 0; left: 0;
            background: rgba(0,0,0,0.5);
            z-index: 1000;
            justify-content: flex-end;
        }

        .cart-panel {
            background: white;
            width: 100%;
            max-width: 400px;
            padding: 20px;
            overflow-y: auto;
        }

        .address-form input, .address-form textarea {
            width: 100%;
            padding: 10px;
            margin: 5px 0;
            border: 1px solid #ddd;
            border-radius: 5px;
        }

        .footer {
            text-align: center;
            padding: 20px;
            background: #0f1825;
            color: white;
            margin-top: 40px;
        }
    </style>
</head>
<body>

<div class="top-bar">
    <div class="header-main">
        <div class="logo"><h1>MallikMart</h1></div>
        <div class="search-bar">
            <input type="text" placeholder="सर्च करें..." id="searchInput">
            <button onclick="filterProducts()">🔍</button>
        </div>
        <div class="nav-icons">
            <div class="cart-icon" id="cartIcon">🛒 कार्ट (<span id="cartCount">0</span>)</div>
        </div>
    </div>
    <div class="category-bar">
        <div class="category-list">
            <span onclick="filterCategory('सभी')">सभी</span>
            <span onclick="filterCategory('मोबाइल')">📱 मोबाइल</span>
            <span onclick="filterCategory('लैपटॉप')">💻 लैपटॉप</span>
            <span onclick="filterCategory('फैशन')">👕 फैशन</span>
        </div>
    </div>
</div>

<div class="container">
    <div class="hero">
        <h2>MallikMart महाबिक्री 🔥</h2>
        <p>70% तक की छूट | कोड: MALLIK2026</p>
    </div>
    <div class="product-grid" id="productGrid"></div>
</div>

<div class="cart-overlay" id="cartOverlay">
    <div class="cart-panel">
        <h3>🛒 आपकी कार्ट</h3>
        <div id="cartItemsList"></div>
        <h4 id="cartTotalValue" style="margin: 20px 0;">कुल: ₹0</h4>
        <div class="address-form">
            <input type="text" id="fullName" placeholder="आपका नाम">
            <input type="tel" id="mobile" placeholder="मोबाइल नंबर">
            <textarea id="address" placeholder="पूरा पता"></textarea>
            <button class="add-btn" onclick="confirmOrder()">ऑर्डर कन्फर्म करें</button>
        </div>
        <button onclick="toggleCart()" style="margin-top:10px; width:100%; padding:8px;">बंद करें</button>
    </div>
</div>

<div class="footer">© 2026 MallikMart | भारत का अपना बाज़ार</div>

<script>
    let products = [
        { id: 1, name: "MallikPhone 13", category: "मोबाइल", price: 28999, image: "📱" },
        { id: 2, name: "MallikBook Air", category: "लैपटॉप", price: 78999, image: "💻" },
        { id: 3, name: "स्पोर्ट्स सूट", category: "फैशन", price: 1299, image: "👕" },
        { id: 4, name: "ब्लूटूथ नेकबैंड", category: "मोबाइल", price: 1199, image: "🎧" },
        { id: 5, name: "स्मार्ट वॉच", category: "मोबाइल", price: 4999, image: "⌚" },
        { id: 6, name: "गेमिंग कीबोर्ड", category: "लैपटॉप", price: 2499, image: "⌨️" }
    ];

    let cart = [];
    let currentCategory = "सभी";

    function renderProducts() {
        let grid = document.getElementById("productGrid");
        let filtered = products.filter(p => currentCategory === "सभी" || p.category === currentCategory);
        grid.innerHTML = filtered.map(p => `
            <div class="product-card">
                <div class="product-img">${p.image}</div>
                <h4>${p.name}</h4>
                <div class="price">₹${p.price.toLocaleString('en-IN')}</div>
                <button class="add-btn" onclick="addToCart(${p.id})">कार्ट में डालें</button>
            </div>
        `).join('');
    }

    function addToCart(id) {
        let p = products.find(i => i.id === id);
        cart.push(p);
        updateCart();
        alert(p.name + " कार्ट में जोड़ा गया!");
    }

    function updateCart() {
        document.getElementById("cartCount").innerText = cart.length;
        let total = cart.reduce((sum, item) => sum + item.price, 0);
        document.getElementById("cartTotalValue").innerText = "कुल: ₹" + total.toLocaleString('en-IN');
        document.getElementById("cartItemsList").innerHTML = cart.map(i => `<p>${i.name} - ₹${i.price}</p>`).join('');
    }

    function toggleCart() {
        let ov = document.getElementById("cartOverlay");
        ov.style.display = ov.style.display === "flex" ? "none" : "flex";
    }

    function filterCategory(cat) {
        currentCategory = cat;
        renderProducts();
    }

    function confirmOrder() {
        let name = document.getElementById("fullName").value;
        if(!name || cart.length === 0) { alert("विवरण भरें और कार्ट चेक करें!"); return; }
        alert("बधाई हो " + name + "! आपका ऑर्डर MallikMart पर दर्ज हो गया है।");
        cart = [];
        updateCart();
        toggleCart();
    }

    document.getElementById("cartIcon").onclick = toggleCart;
    renderProducts();
</script>
</body>
</html>
