<!DOCTYPE html>
<html lang="de">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="description" content="Amazon ähnliche E-Commerce Website">
  <title>Mein Shop</title>
  <link rel="stylesheet" href="styles.css">
</head>
<body>

  <!-- Header mit Navigation -->
  <header>
    <div class="logo">Mein Shop</div>
    <div class="search-bar">
      <input type="text" id="search" placeholder="Suche nach Produkten..." onkeyup="searchProducts()">
    </div>
    <div class="cart" onclick="toggleCart()">
      🛒 Warenkorb (<span id="cart-count">0</span>)
    </div>
  </header>

  <!-- Produktliste -->
  <section id="products" class="products">
    <h2>Unsere Produkte</h2>
    <div class="product" data-name="Laptop">
      <img src="https://via.placeholder.com/200x200" alt="Laptop">
      <h3>Laptop</h3>
      <p class="price">€799</p>
      <button onclick="addToCart('Laptop', 799)">In den Warenkorb</button>
    </div>
    <div class="product" data-name="Smartphone">
      <img src="https://via.placeholder.com/200x200" alt="Smartphone">
      <h3>Smartphone</h3>
      <p class="price">€599</p>
      <button onclick="addToCart('Smartphone', 599)">In den Warenkorb</button>
    </div>
    <div class="product" data-name="Tablet">
      <img src="https://via.placeholder.com/200x200" alt="Tablet">
      <h3>Tablet</h3>
      <p class="price">€499</p>
      <button onclick="addToCart('Tablet', 499)">In den Warenkorb</button>
    </div>
    <div class="product" data-name="Kopfhörer">
      <img src="https://via.placeholder.com/200x200" alt="Kopfhörer">
      <h3>Kopfhörer</h3>
      <p class="price">€199</p>
      <button onclick="addToCart('Kopfhörer', 199)">In den Warenkorb</button>
    </div>
  </section>

  <!-- Warenkorb Popup -->
  <div id="cart-popup" class="cart-popup">
    <h3>Warenkorb</h3>
    <ul id="cart-items"></ul>
    <p id="cart-total">Gesamt: €0</p>
    <button onclick="checkout()">Zur Kasse</button>
    <button onclick="clearCart()">Warenkorb leeren</button>
    <button onclick="toggleCart()">Schließen</button>
  </div>

  <footer>
    <p>&copy; 2025 Mein Shop</p>
  </footer>

  <script src="scripts.js"></script>
</body>
</html>
/* Allgemeine Styles */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: Arial, sans-serif;
  background-color: #f4f4f4;
  color: #333;
}

header {
  background-color: #333;
  color: white;
  display: flex;
  justify-content: space-between;
  padding: 20px;
  align-items: center;
}

header .logo {
  font-size: 2rem;
}

header .search-bar input {
  padding: 10px;
  border-radius: 4px;
  border: 1px solid #ddd;
}

header .cart {
  cursor: pointer;
}

.products {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
  padding: 20px;
}

.product {
  background-color: white;
  width: 200px;
  padding: 15px;
  margin: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  text-align: center;
  border-radius: 8px;
}

.product img {
  width: 100%;
  border-radius: 8px;
}

.product button {
  margin-top: 10px;
  padding: 10px;
  background-color: #28a745;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.product button:hover {
  background-color: #218838;
}

/* Warenkorb Popup */
.cart-popup {
  position: fixed;
  top: 0;
  right: 0;
  background-color: white;
  width: 300px;
  height: 100%;
  padding: 20px;
  box-shadow: -4px 0 8px rgba(0, 0, 0, 0.1);
  display: none;
  flex-direction: column;
}

.cart-popup ul {
  list-style-type: none;
  padding-left: 0;
}

.cart-popup li {
  margin-bottom: 10px;
}

footer {
  text-align: center;
  padding: 20px;
  background-color: #333;
  color: white;
}

button {
  cursor: pointer;
}

button:hover {
  opacity: 0.8;
}
let cart = [];
let cartCount = document.getElementById('cart-count');
let cartItems = document.getElementById('cart-items');
let cartTotal = document.getElementById('cart-total');
let cartPopup = document.getElementById('cart-popup');

// Produkt zum Warenkorb hinzufügen
function addToCart(productName, price) {
  const product = {
    name: productName,
    price: price
  };
  cart.push(product);
  updateCart();
}

// Warenkorb aktualisieren
function updateCart() {
  // Aktualisiere die Anzahl im Warenkorb
  cartCount.innerText = cart.length;
  
  // Aktualisiere die Liste im Warenkorb
  cartItems.innerHTML = '';
  let total = 0;
  cart.forEach(item => {
    const listItem = document.createElement('li');
    listItem.textContent = `${item.name} - €${item.price}`;
    cartItems.appendChild(listItem);
    total += item.price;
  });
  
  // Aktualisiere den Gesamtpreis
  cartTotal.innerText = `Gesamt: €${total}`;
}

// Warenkorb anzeigen oder verstecken
function toggleCart() {
  cartPopup.style.display = cartPopup.style.display === 'none' ? 'flex' : 'none';
}

// Kasse
function checkout() {
  alert('Kasse abgeschlossen! Vielen Dank für deinen Einkauf.');
  clearCart();
}

// Warenkorb leeren
function clearCart() {
  cart = [];
  updateCart();
  toggleCart();
}

// Produkte nach Namen filtern
function searchProducts() {
  const searchTerm = document.getElementById('search').value.toLowerCase();
  const products = document.querySelectorAll('.product');
  
  products.forEach(product => {
    const productName = product.getAttribute('data-name').toLowerCase();
    if (productName.includes(searchTerm)) {
      product.style.display = 'block';
    } else {
      product.style.display = 'none';
    }
  });
}
