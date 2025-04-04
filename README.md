<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Molly Toyhouse - Blind Box & Art Toys</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #F0F8FF;
            color: #333;
            text-align: center;
        }
        header {
            background-color: #007BFF;
            color: white;
            padding: 20px;
            font-size: 24px;
        }
        .container {
            width: 80%;
            margin: auto;
            padding: 20px;
        }
        .product {
            border: 1px solid #ddd;
            padding: 10px;
            margin: 10px;
            display: inline-block;
            width: 250px;
            background: white;
        }
        .product img {
            width: 100%;
            height: auto;
        }
        .buttons {
            margin-top: 20px;
        }
        .buttons a {
            text-decoration: none;
            padding: 10px 20px;
            margin: 5px;
            display: inline-block;
            color: white;
            border-radius: 5px;
        }
        .fb {
            background-color: #3b5998;
        }
        .shopee {
            background-color: #ee4d2d;
        }
        .form-container {
            margin: 20px auto;
            padding: 20px;
            background: white;
            width: 50%;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0,0,0,0.1);
        }
        input, button {
            padding: 10px;
            margin: 5px;
            width: 90%;
        }
    </style>
</head>
<body>
    <header>Molly Toyhouse - Blind Box & Art Toys</header>
    
    <div class="container">
        <h2>Sản phẩm mới nhất</h2>
        <div id="product-list"></div>
    </div>
    
    <div class="form-container">
        <h3>Thêm sản phẩm mới</h3>
        <input type="text" id="product-name" placeholder="Tên sản phẩm">
        <input type="text" id="product-img" placeholder="URL hình ảnh">
        <input type="text" id="product-link" placeholder="Link Shopee">
        <button onclick="addProduct()">Thêm sản phẩm</button>
    </div>
    
    <div class="buttons">
        <a href="https://www.facebook.com/MollyToyhouse" class="fb">Facebook</a>
        <a href="https://shopee.vn/mollytoyhouse" class="shopee">Shopee</a>
    </div>
    
    <script>
        let products = JSON.parse(localStorage.getItem("products")) || [
            {name: "Blind Box 1", img: "https://via.placeholder.com/250", link: "https://shopee.vn/product1"},
            {name: "Blind Box 2", img: "https://via.placeholder.com/250", link: "https://shopee.vn/product2"},
            {name: "Blind Box 3", img: "https://via.placeholder.com/250", link: "https://shopee.vn/product3"}
        ];
        
        function renderProducts() {
            const productList = document.getElementById("product-list");
            productList.innerHTML = "";
            products.forEach((product, index) => {
                const productDiv = document.createElement("div");
                productDiv.className = "product";
                productDiv.innerHTML = `
                    <img src="${product.img}" alt="${product.name}">
                    <h3>${product.name}</h3>
                    <a href="${product.link}" class="shopee">Mua ngay</a>
                    <br>
                    <button onclick="removeProduct(${index})">Xóa</button>
                `;
                productList.appendChild(productDiv);
            });
        }
        
        function addProduct() {
            const name = document.getElementById("product-name").value;
            const img = document.getElementById("product-img").value;
            const link = document.getElementById("product-link").value;
            
            if (name && img && link) {
                products.push({ name, img, link });
                localStorage.setItem("products", JSON.stringify(products));
                renderProducts();
            }
        }
        
        function removeProduct(index) {
            products.splice(index, 1);
            localStorage.setItem("products", JSON.stringify(products));
            renderProducts();
        }
        
        renderProducts();
    </script>
</body>
</html>
