HTML
<!DOCTYPE html>
<html lang="ka">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Catering Premium | ონლაინ შეკვეთა</title>
    <style>
        :root {
            --primary-color: #1a252c;
            --accent-color: #c5a059;
            --bg-color: #f8f9fa;
            --card-bg: #ffffff;
            --text-color: #333333;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background-color: var(--bg-color);
            color: var(--text-color);
        }

        /* Header */
        header {
            background-color: var(--primary-color);
            color: white;
            padding: 1rem 2rem;
            position: sticky;
            top: 0;
            z-index: 100;
            display: flex;
            justify-content: space-between;
            align-items: center;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }

        .logo {
            font-size: 1.5rem;
            font-weight: bold;
            color: var(--accent-color);
            letter-spacing: 1px;
        }

        .cart-btn {
            background-color: var(--accent-color);
            color: white;
            border: none;
            padding: 0.6rem 1.2rem;
            border-radius: 20px;
            cursor: pointer;
            font-weight: bold;
            transition: background 0.3s;
        }

        .cart-btn:hover {
            background-color: #b08d46;
        }

        /* Hero Banner */
        .hero {
            background: linear-gradient(rgba(0,0,0,0.6), rgba(0,0,0,0.6)), url('https://images.unsplash.com/photo-1555244162-803834f70033?auto=format&fit=crop&w=1350&q=80');
            background-size: cover;
            background-position: center;
            color: white;
            text-align: center;
            padding: 5rem 1rem;
        }

        .hero h1 {
            font-size: 2.5rem;
            margin-bottom: 1rem;
        }

        .hero p {
            font-size: 1.2rem;
            color: #ddd;
        }

        /* Menu Section */
        .container {
            max-width: 1200px;
            margin: 2rem auto;
            padding: 0 1rem;
        }

        .section-title {
            text-align: center;
            margin-bottom: 2rem;
            color: var(--primary-color);
            font-size: 2rem;
        }

        .grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 2rem;
        }

        .card {
            background: var(--card-bg);
            border-radius: 12px;
            overflow: hidden;
            box-shadow: 0 4px 15px rgba(0,0,0,0.05);
            transition: transform 0.3s;
            display: flex;
            flex-direction: column;
        }

        .card:hover {
            transform: translateY(-5px);
        }

        .card img {
            width: 100%;
            height: 200px;
            object-fit: cover;
        }

        .card-content {
            padding: 1.5rem;
            display: flex;
            flex-direction: column;
            flex-grow: 1;
        }

        .card-title {
            font-size: 1.25rem;
            margin-bottom: 0.5rem;
        }

        .card-desc {
            color: #666;
            font-size: 0.9rem;
            margin-bottom: 1rem;
            flex-grow: 1;
        }

        .card-footer {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-top: auto;
        }

        .price {
            font-size: 1.2rem;
            font-weight: bold;
            color: var(--primary-color);
        }

        .add-btn {
            background-color: var(--primary-color);
            color: white;
            border: none;
            padding: 0.5rem 1rem;
            border-radius: 6px;
            cursor: pointer;
            transition: background 0.3s;
        }

        .add-btn:hover {
            background-color: var(--accent-color);
        }

        /* Modal / Cart */
        .modal {
            display: none;
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(0,0,0,0.5);
            justify-content: center;
            align-items: center;
            z-index: 1000;
        }

        .modal-content {
            background: white;
            padding: 2rem;
            border-radius: 12px;
            width: 90%;
            max-width: 500px;
            max-height: 80vh;
            overflow-y: auto;
        }

        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 1rem;
        }

        .close-btn {
            cursor: pointer;
            font-size: 1.5rem;
        }

        .cart-item {
            display: flex;
            justify-content: space-between;
            padding: 0.5rem 0;
            border-bottom: 1px solid #eee;
        }

        .checkout-form {
            margin-top: 1.5rem;
            display: flex;
            flex-direction: column;
            gap: 0.8rem;
        }

        .checkout-form input {
            padding: 0.8rem;
            border: 1px solid #ccc;
            border-radius: 6px;
        }

        .submit-btn {
            background-color: var(--accent-color);
            color: white;
            padding: 0.8rem;
            border: none;
            border-radius: 6px;
            font-weight: bold;
            cursor: pointer;
        }
    </style>
</head>
<body>

    <header>
        <div class="logo">LUX CATERING</div>
        <button class="cart-btn" onclick="toggleCart()">კალათა (<span id="cart-count">0</span>)</button>
    </header>

    <section class="hero">
        <h1>პრემიუმ ქეთერინგის მომსახურება</h1>
        <p>დაუკვეთეთ დახვეწილი კერძები და ფურშეტები თქვენი ღონისძიებისთვის</p>
    </section>

    <div class="container">
        <h2 class="section-title">ჩვენი მენიუ</h2>
        <div class="grid" id="product-grid">
            <!-- პროდუქტები ჩაიტვირთება JS-ით -->
        </div>
    </div>

    <!-- კალათის მოდალური ფანჯარა -->
    <div class="modal" id="cart-modal">
        <div class="modal-content">
            <div class="modal-header">
                <h3>თქვენი შეკვეთა</h3>
                <span class="close-btn" onclick="toggleCart()">&times;</span>
            </div>
            <div id="cart-items">
                <!-- კალათის ელემენტები -->
            </div>
            <h4 style="margin-top: 1rem;">სულ: <span id="cart-total">0</span> €</h4>
            
            <form class="checkout-form" onsubmit="handleCheckout(event)">
                <input type="text" placeholder="თქვენი სახელი" required>
                <input type="tel" placeholder="ტელეფონის ნომერი" required>
                <input type="text" placeholder="მიწოდების მისამართი" required>
                <button type="submit" class="submit-btn">შეკვეთის გაფორმება</button>
            </form>
        </div>
    </div>

    <script>
        const products = [
            { id: 1, name: "კანაპეს ნაკრები Premium", price: 45, desc: "24 ცალი მრავალფეროვანი კანაპე ზღვის პროდუქტებითა და ყველის ასორტით.", img: "https://images.unsplash.com/photo-1541529086526-db283c563270?auto=format&fit=crop&w=500&q=80" },
            { id: 2, name: "მინი ბურგერების სეტი", price: 35, desc: "12 ცალი წვნიანი მინი ბურგერი საქონლის ხორცითა და ჩედარით.", img: "https://images.unsplash.com/photo-1568901346375-23c9450c58cd?auto=format&fit=crop&w=500&q=80" },
            { id: 3, name: "ფურშეტის დესერტების დაფა", price: 40, desc: "16 ცალი ტრადიციული და თანამედროვე მინი დესერტი.", img: "https://images.unsplash.com/photo-1551024709-8f23befc6f87?auto=format&fit=crop&w=500&q=80" },
            { id: 4, name: "ესპანური Tapas & Jamón Box", price: 55, desc: "ხამონი, ადგილობრივი ყველეული, ოლივები და ხრაშუნა პური.", img: "https://images.unsplash.com/photo-1544025162-d76694265947?auto=format&fit=crop&w=500&q=80" }
        ];

        let cart = [];

        function renderProducts() {
            const grid = document.getElementById('product-grid');
            grid.innerHTML = products.map(p => `
                <div class="card">
                    <img src="${p.img}" alt="${p.name}">
                    <div class="card-content">
                        <div class="card-title">${p.name}</div>
                        <div class="card-desc">${p.desc}</div>
                        <div class="card-footer">
                            <div class="price">${p.price} €</div>
                            <button class="add-btn" onclick="addToCart(${p.id})">დამატება</button>
                        </div>
                    </div>
                </div>
            `).join('');
        }

        function addToCart(id) {
            const product = products.find(p => p.id === id);
            cart.push(product);
            updateCart();
        }

        function updateCart() {
            document.getElementById('cart-count').innerText = cart.length;
            const cartItems = document.getElementById('cart-items');
            cartItems.innerHTML = cart.map((item, index) => `
                <div class="cart-item">
                    <span>${item.name}</span>
                    <span>${item.price} €</span>
                </div>
            `).join('');
            
            const total = cart.reduce((sum, item) => sum + item.price, 0);
            document.getElementById('cart-total').innerText = total;
        }

        function toggleCart() {
            const modal = document.getElementById('cart-modal');
            modal.style.display = modal.style.display === 'flex' ? 'none' : 'flex';
        }

        function handleCheckout(e) {
            e.preventDefault();
            if(cart.length === 0) {
                alert('კალათა ცარიელია!');
                return;
            }
            alert('გმადლობთ შეკვეთისთვის! ჩვენ მალე დაგიკავშირდებით.');
            cart = [];
            updateCart();
            toggleCart();
        }

        renderProducts();
    </script>
</body>
</html>
