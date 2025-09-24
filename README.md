# Dynamic-Product-Filter-with-DOM-Manipulation
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Dynamic Product Filter</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      padding: 20px;
    }
    select {
      margin-bottom: 20px;
      padding: 8px 12px;
      font-size: 16px;
    }
    #products-container {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
      gap: 15px;
    }
    .product {
      border: 1px solid #ccc;
      padding: 15px;
      border-radius: 10px;
      text-align: center;
      box-shadow: 0px 2px 6px rgba(0,0,0,0.1);
      transition: transform 0.2s ease;
    }
    .product:hover {
      transform: scale(1.05);
    }
    .product h3 {
      margin: 10px 0;
    }
    .product p {
      font-size: 18px;
      font-weight: bold;
      color: green;
    }
  </style>
</head>
<body>
  <h2>Dynamic Product Filter</h2>
  
  <!-- Dropdown Filter -->
  <select id="filter">
    <option value="all">All Products</option>
    <option value="electronics">Electronics</option>
    <option value="clothing">Clothing</option>
  </select>

  <!-- Container for Products -->
  <div id="products-container"></div>

  <script>
    // Product Dataset
    const products = [
      { name: "Laptop", category: "electronics", price: 999 },
      { name: "Shirt", category: "clothing", price: 25 },
      { name: "Headphones", category: "electronics", price: 199 },
      { name: "Jeans", category: "clothing", price: 45 },
      { name: "Smartphone", category: "electronics", price: 799 }
    ];

    // Event Listener for Dropdown
    document.getElementById('filter').addEventListener('change', (e) => {
      const selected = e.target.value;
      const filtered = selected === 'all' ? products : products.filter(p => p.category === selected);
      renderProducts(filtered);
    });

    // Render Function
    function renderProducts(products) {
      const container = document.getElementById('products-container');
      if (products.length === 0) {
        container.innerHTML = "<p>No products available.</p>";
        return;
      }
      container.innerHTML = products.map(p => `
        <div class="product">
          <h3>${p.name}</h3>
          <p>$${p.price}</p>
        </div>
      `).join('');
    }

    // Initial Render
    renderProducts(products);
  </script>
</body>
</html>
