# apple-store-html

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Apple Store - iPhone Collection (Interactive)</title>
  <style>
    body {
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
        Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
      background: #f5f5f7;
      margin: 0;
      padding: 20px;
      text-align: center;
      color: #1d1d1f;
    }
    h1 {
      font-weight: 700;
      margin-bottom: 10px;
    }
    .cart {
      background: #fff;
      border-radius: 10px;
      box-shadow: 0 4px 15px rgb(0 0 0 / 0.1);
      padding: 15px 20px;
      max-width: 1200px;
      margin: 0 auto 30px auto;
      text-align: left;
      font-size: 16px;
      position: sticky;
      top: 0;
      z-index: 10;
    }
    .cart h2 {
      margin: 0 0 10px 0;
      font-size: 20px;
    }
    .cart-items {
      margin-bottom: 10px;
    }
    .cart-item {
      display: flex;
      justify-content: space-between;
      padding: 6px 0;
      border-bottom: 1px solid #ddd;
    }
    .cart-total {
      font-weight: 700;
      font-size: 18px;
      margin-top: 10px;
    }
    .btn-clear {
      background: #fa3e3e;
      color: white;
      border: none;
      padding: 6px 12px;
      border-radius: 6px;
      cursor: pointer;
      font-weight: 600;
    }
    .container {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      gap: 25px;
      max-width: 1200px;
      margin: 0 auto;
    }
    .phone-card {
      background: white;
      border-radius: 15px;
      box-shadow: 0 4px 15px rgb(0 0 0 / 0.1);
      width: 280px;
      padding: 20px;
      text-align: left;
      transition: transform 0.3s ease;
      display: flex;
      flex-direction: column;
      justify-content: space-between;
    }
    .phone-card:hover {
      transform: scale(1.05);
    }
    .phone-img {
      width: 100%;
      border-radius: 12px;
      object-fit: contain;
      margin-bottom: 15px;
    }
    .phone-name {
      font-size: 20px;
      font-weight: 700;
      margin-bottom: 5px;
    }
    .phone-price {
      color: #fa3e3e;
      font-weight: 600;
      font-size: 18px;
      margin-bottom: 10px;
    }
    .phone-specs {
      font-size: 14px;
      line-height: 1.5;
      color: #555;
      margin-bottom: 15px;
    }
    .btn-buy {
      background: #0071e3;
      color: white;
      border: none;
      padding: 10px;
      border-radius: 10px;
      cursor: pointer;
      font-weight: 700;
      transition: background-color 0.3s ease;
    }
    .btn-buy:hover {
      background-color: #005bb5;
    }
    @media (max-width: 768px) {
      .container {
        flex-direction: column;
        align-items: center;
      }
      .cart {
        position: static;
        margin-bottom: 20px;
      }
    }
    h2.section-title {
      width: 100%;
      margin-top: 50px;
      border-bottom: 2px solid #ccc;
      padding-bottom: 10px;
      color: #333;
    }
  </style>
</head>
<body>

  <h1>Apple Store - iPhone Collection</h1>

  <div class="cart" id="cart">
    <h2>Shopping Cart</h2>
    <div class="cart-items" id="cart-items">Your cart is empty.</div>
    <div class="cart-total" id="cart-total"></div>
    <button class="btn-clear" id="clear-cart">Clear Cart</button>
  </div>

  <div class="container" id="phone-list">

    <!-- Phones will be injected here by JavaScript -->

  </div>

  <h2 class="section-title">Upcoming 2025 iPhone Models</h2>

  <div class="container" id="phone-list-2025">

    <!-- 2025 phones injected here -->

  </div>

  <script>
    // Phone Data (existing + 2025 models)
    const phones = [
      {
        id: 1,
        name: "iPhone 14 Pro",
        price: 129900,
        img: "https://store.storeimages.cdn-apple.com/4668/as-images.apple.com/is/iphone-14-pro-family-hero-all?wid=470&hei=556&fmt=png-alpha&.v=1660753619946",
        specs: "Display: 6.1-inch Super Retina XDR<br>Processor: A16 Bionic chip<br>Camera: 48MP Triple-lens<br>Battery: Up to 23 hours video playback",
        section: "existing",
      },
      {
        id: 2,
        name: "iPhone 14",
        price: 79900,
        img: "https://store.storeimages.cdn-apple.com/4668/as-images.apple.com/is/iphone-14-family-hero-all?wid=470&hei=556&fmt=png-alpha&.v=1660753619936",
        specs: "Display: 6.1-inch Super Retina XDR<br>Processor: A15 Bionic chip<br>Camera: 12MP Dual-lens<br>Battery: Up to 20 hours video playback",
        section: "existing",
      },
      {
        id: 3,
        name: "iPhone 13 Pro",
        price: 119900,
        img: "https://store.storeimages.cdn-apple.com/4668/as-images.apple.com/is/iphone-13-pro-family-select-2021?wid=470&hei=556&fmt=png-alpha&.v=1645552346281",
        specs: "Display: 6.1-inch Super Retina XDR<br>Processor: A15 Bionic chip<br>Camera: 12MP Triple-lens<br>Battery: Up to 22 hours video playback",
        section: "existing",
      },
      {
        id: 4,
        name: "iPhone SE (2022)",
        price: 43900,
        img: "https://store.storeimages.cdn-apple.com/4668/as-images.apple.com/is/iphone-se-2022-family-hero?wid=470&hei=556&fmt=png-alpha&.v=1645069385433",
        specs: "Display: 4.7-inch Retina HD<br>Processor: A15 Bionic chip<br>Camera: 12MP Single-lens<br>Battery: Up to 15 hours video playback",
        section: "existing",
      },
      {
        id: 5,
        name: "iPhone 12",
        price: 59900,
        img: "https://store.storeimages.cdn-apple.com/4668/as-images.apple.com/is/iphone-12-family-select-2021?wid=470&hei=556&fmt=png-alpha&.v=1631848472000",
        specs: "Display: 6.1-inch Super Retina XDR<br>Processor: A14 Bionic chip<br>Camera: 12MP Dual-lens<br>Battery: Up to 17 hours video playback",
        section: "existing",
      }
    ];

    const phones2025 = [
      {
        id: 6,
        name: "iPhone 15 Pro",
        price: 139900,
        img: "https://fakeimg.pl/470x556/000/fff/?text=iPhone+15+Pro&font=lobster",
        specs: "Display: 6.1-inch ProMotion LTPO OLED<br>Processor: A17 Bionic chip<br>Camera: 48MP Triple-lens with improved zoom<br>Battery: Up to 24 hours video playback",
      },
      {
        id: 7,
        name: "iPhone 15",
        price: 89900,
        img: "https://fakeimg.pl/470x556/222/eee/?text=iPhone+15&font=lobster",
        specs: "Display: 6.1-inch OLED<br>Processor: A16 Bionic chip<br>Camera: 12MP Dual-lens with better low light<br>Battery: Up to 22 hours video playback",
      },
      {
        id: 8,
        name: "iPhone 15 Plus",
        price: 99900,
        img: "https://fakeimg.pl/470x556/555/ddd/?text=iPhone+15+Plus&font=lobster",
        specs: "Display: 6.7-inch OLED<br>Processor: A16 Bionic chip<br>Camera: 12MP Dual-lens<br>Battery: Up to 26 hours video playback",
      },
      {
        id: 9,
        name: "iPhone 15 Pro Max",
        price: 169900,
        img: "https://fakeimg.pl/470x556/111/eee/?text=iPhone+15+Pro+Max&font=lobster",
        specs: "Display: 6.7-inch ProMotion LTPO OLED<br>Processor: A17 Bionic chip<br>Camera: 48MP Triple-lens with advanced zoom<br>Battery: Up to 29 hours video playback",
      }
    ];

    const cart = [];

    // Format price in INR with commas
    function formatPrice(num) {
      return '₹' + num.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");
    }

    function renderPhones() {
      const phoneList = document.getElementById("phone-list");
      phones.forEach(phone => {
        const card = document.createElement("div");
        card.className = "phone-card";
        card.innerHTML = `
          <img src="${phone.img}" alt="${phone.name}" class="phone-img" />
          <div class="phone-name">${phone.name}</div>
          <div class="phone-price">${formatPrice(phone.price)}</div>
          <div class="phone-specs">${phone.specs}</div>
          <button class="btn-buy" onclick="addToCart(${phone.id}, '${phone.name}', ${phone.price})">Buy Now</button>
        `;
        phoneList.appendChild(card);
      });
    }

    function renderPhones2025() {
      const phoneList2025 = document.getElementById("phone-list-2025");
      phones2025.forEach(phone => {
        const card = document.createElement("div");
        card.className = "phone-card";
        card.innerHTML = `
          <img src="${phone.img}" alt="${phone.name}" class="phone-img" />
          <div class="phone-name">${phone.name}</div>
          <div class="phone-price">${formatPrice(phone.price)}</div>
          <div class="phone-specs">${phone.specs}</div>
          <button class="btn-buy" onclick="addToCart(${phone.id}, '${phone.name}', ${phone.price})">Buy Now</button>
        `;
        phoneList2025.appendChild(card);
      });
    }

    function addToCart(id, name, price) {
      const existing = cart.find(item => item.id === id);
      if (existing) {
        existing.qty++;
      } else {
        cart.push({id, name, price, qty: 1});
      }
      renderCart();
    }

    function renderCart() {
      const cartItems = document.getElementById("cart-items");
      const cartTotal = document.getElementById("cart-total");

      if (cart.length === 0) {
        cartItems.innerHTML = "Your cart is empty.";
        cartTotal.innerHTML = "";
        return;
      }

      cartItems.innerHTML = "";
      let total = 0;
      cart.forEach(item => {
        const div = document.createElement("div");
        div.className = "cart-item";
        div.innerHTML = `
          <div>${item.name} x${item.qty}</div>
          <div>${formatPrice(item.price * item.qty)}</div>
        `;
        cartItems.appendChild(div);
        total += item.price * item.qty;
      });
      cartTotal.innerHTML = `Total: <strong>${formatPrice(total)}</strong>`;
    }

    function clearCart() {
      cart.length = 0;
      renderCart();
    }

    document.getElementById("clear-cart").addEventListener("click", clearCart);

    // Initial render
    renderPhones();
    renderPhones2025();
    renderCart();
  </script>

</body>
</html>
