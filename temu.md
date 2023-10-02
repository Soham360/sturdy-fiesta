---
layout: base
permalink: /temu/
title: Temu
---

<html>
    <head>
        <title>Temu</title>
        <style>
            body {
            font-family: sans-serif;
            }
            .header {
            background-color: #fff;
            padding: 20px;
            }
            .logo {
            float: left;
            width: 200px;
            height: 100px;
            }
            .search-bar {
            float: right;
            width: 500px;
            }
            .nav {
            background-color: #fff;
            padding: 10px;
            }
            .nav-item {
            float: left;
            padding: 10px;
            }
            .main {
            padding: 20px;
            }
            .product-list {
            list-style-type: none;
            padding: 0;
            }
            .product-item {
            float: left;
            width: 200px;
            height: 300px;
            margin: 10px;
            }
            .product-image {
            width: 100%;
            height: 200px;
            }
            .product-name {
            font-size: 16px;
            padding: 10px;
            }
            .product-price {
            font-size: 14px;
            padding: 10px;
            }
            .footer {
            background-color: #fff;
            padding: 20px;
            }
            .copyright {
            text-align: center;
            }
        </style>
        </head>
    <body>
        <header>
            <div class="logo">
                <img src="https://github.com/Soham360/sturdy-fiesta/blob/master/images/Temu_logo.png?raw=true" alt="Temu logo">
            </div>
            <div class="search-bar">
                <input type="text" placeholder="Search for products...">
                <button type="submit">Search</button>
            </div>
        </header>
        <nav>
            <a class="nav-item" href="#">Home</a>
            <a class="nav-item" href="#">Categories</a>
            <a class="nav-item" href="#">Deals</a>
            <a class="nav-item" href="#">My Cart</a>
        </nav>
        <main>
            <div class="product-list">
                <div class="product-item">
                    <img class="product-image" src="https://i.imgur.com/product-1.jpg" alt="Product 1">
                    <h3 class="product-name">Product 1</h3>
                    <h4 class="product-price">$9.99</h4>
                </div>
                <div class="product-item">
                    <img class="product-image" src="https://i.imgur.com/product-2.jpg" alt="Product 2">
                    <h3 class="product-name">Product 2</h3>
                    <h4 class="product-price">$19.99</h4>
                </div>
                <div class="product-item">
                    <img class="product-image" src="https://i.imgur.com/product-3.jpg" alt="Product 3">
                    <h3 class="product-name">Product 3</h3>
                    <h4 class="product-price">$29.99</h4>
                </div>
            </div>
        </main>
    </body>
</html>
