<!DOCTYPE html>
<html lang="en">
<head>
  <!-- ... (same head as before) -->
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Apple Store - iPhone Collection (Buy Now with Links)</title>
  <style>
    /* same CSS as before */
    body {
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
        Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
      background: #f5f5f7;
      margin: 0;
      padding: 20px;
      text-align: center;
      color: #1d1d1f;
    }
    /* ... (rest of the CSS unchanged) */
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

  <div class="container" id="phone-list"></div>

  <h2 class="section-title">Upcoming 2025 iPhone Models</h2>

  <div class="container" id="phone-list-2025"></div>

  <script>
    // Phone Data with Amazon Links
    const phones = [
      {
        id: 1,
        name: "iPhone 14 Pro",
        price: 129900,
        img: "https://store.storeimages.cdn-apple.com/4668/as-images.apple.com/is/iphone-14-pro-family-hero-all?wid=470&hei=556&fmt=png-alpha&.v=1660753619946",
        specs: "Display: 6.1-inch Super Retina XDR<br>Processor: A16 Bionic chip<br>Camera: 48MP Triple-lens<br>Battery: Up to 23 hours video playback",
        amazonLink: "https://www.amazon.in/s?k=iphone+14+pro",
        section: "existing",
      },
      {
        id: 2,
        name: "iPhone 14",
        price: 79900,
        img: "https://store.storeimages.cdn-apple.com/4668/as-images.apple.com/is/iphone-14-family-hero-all?wid=470&hei=556&fmt=png-alpha&.v=1660753619936",
        specs: "Display: 6.1-inch Super Retina XDR<br>Processor: A15 Bionic chip<br>Camera: 12MP Dual-lens<br>Battery: Up to 20 hours video playback",
        amazonLink: "https://www.amazon.in/s?k=iphone+14",
        section: "existing",
      },
      {
        id: 3,
        name: "iPhone 13 Pro",
        price: 119900,
        img: "https://store.storeimages.cdn-apple.com/4668/as-images.apple.com/is/iphone-13-pro-family-select-2021?wid=470&hei=556&fmt=png-alpha&.v=1645552346281",
        specs: "Display: 6.1-inch Super Retina XDR<br>Processor: A15 Bionic chip<br>Camera: 12MP Triple-lens<br>Battery: Up to 22 hours video playback",
        amazonLink: "https://www.amazon.in/s?k=iphone+13+pro",
        section: "existing",
      },
      {
        id: 4,
        name: "iPhone SE (2022)",
        price: 43900,
        img: "https://store.storeimages.cdn-apple.com/4668/as-images.apple.com/is/iphone-se-2022-family-hero?wid=470&hei=556&fmt=png-alpha&.v=1645069385433",
        specs: "Display: 4.7-inch Retina HD<br>Processor: A15 Bionic chip<br>Camera: 12MP Single-lens<br>Battery: Up to 15 hours video playback",
        amazonLink: "https://www.amazon.in/s?k=iphone+se+2022",
        section: "existing",
      },
      {
        id: 5,
        name: "iPhone 12",
        price: 59900,
        img: "https://store.storeimages.cdn-apple.com/4668/as-images.apple.com/is/iphone-12-family-select-2021?wid=470&hei=556&fmt=png-alpha&.v=1631848472000",
        specs: "Display: 6.1-inch Super Retina XDR<br>Processor: A14 Bionic chip<br>Camera: 12MP Dual-lens<br>Battery: Up to 17 hours video playback",
        amazonLink: "https://www.amazon.in/s?k=iphone+12",
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
        amazonLink: "https://www.amazon.in/s?k=iphone+15+pro",
      },
      {
        id: 7,
        name: "iPhone 15",
        price: 89900,
        img: "https://fakeimg.pl/470x556/222/eee/?text=iPhone+15&font=lobster",
        specs: "Display: 6.1-inch OLED<br>Processor: A16 Bionic chip<br>Camera: 12MP Dual-lens with better low light<br>Battery: Up to 22 hours video playback",
        amazonLink: "https://www.amazon.in/s?k=iphone+15",
      },
      {
        id: 8,
        name: "iPhone 15 Plus",
        price: 99900,
        img: "https://fakeimg.pl/470x556/555/ddd/?text=iPhone+15+Plus&font=lobster",
        specs: "Display: 6.7-inch OLED<br>Processor: A16 Bionic chip<br>Camera: 12MP Dual-lens<br>Battery: Up to 26 hours video playback",
        amazonLink: "https://www.amazon.in/s?k=iphone+15+plus",
      },
      {
        id: 9,
        name: "iPhone 15 Pro Max",
        price: 169900,
        img: "https://fakeimg.pl/470x556/111/eee/?text=iPhone+15+Pro+Max&font=lobster",
        specs: "Display: 6.7-inch ProMotion LTPO OLED<br>Processor: A17 Bionic chip<br>Camera: 48MP Triple-lens with advanced zoom<br>Battery: Up to 29 hours video playback",
        amazonLink: "https://www.amazon.in/s?k=iphone+15+pro+max",
      }
    ];

    const cart = [];

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
          <button class="btn-buy" onclick="buyNow(${phone.id})">Buy Now</button>
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
          <button class="btn-buy" onclick="buyNow(${phone.id}, true)">Buy Now</button>
        `;
        phoneList2025.appendChild(card);
      });
    }

    // Modified addToCart & open link in new tab
    function buyNow(id, is2025 = false) {
      let phone;
      if(is2025){
        phone = phones2025.find(p => p.id === id);
      } else {
        phone = phones.find(p => p.id === id);
      }

      if(!phone) return;

      // Add to cart
      const existing = cart.find(item => item.id === phone.id);
      if (existing) {
        existing.qty++;
      } else {
        cart.push({id: phone.id, name: phone.name, price: phone.price, qty: 1});
      }
      renderCart();

      // Open Amazon link in new tab
      if (phone.amazonLink) {
        window.open(phone.amazonLink, "_blank");
      }
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
