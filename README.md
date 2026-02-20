# Vue Shop - Mini E-Commerce Project

![Vue](https://img.shields.io/badge/Vue-3.x-brightgreen)
![Pinia](https://img.shields.io/badge/Pinia-State-blue)
![TailwindCSS](https://img.shields.io/badge/TailwindCSS-CSS-blueviolet)

A simple Vue 3 e-commerce project with **Products listing**, **Product details**, and **Shopping cart** using **Vue
Router**, **Pinia**, and **TailwindCSS**.


https://hamedabdollahzade.github.io/vue-shop/
---

## 🎯 Features

### Products Page

- Display a list of products (mock data)
- Search products by name
- Filter products by category
- Responsive grid layout with TailwindCSS
- Navigate to product details page

### Product Detail Page

- Dynamic route (`/products/:id`)
- Display full product info: title, price, description, image
- Add product to shopping cart
- Back to products list

### Shopping Cart

- View cart items
- Remove items from cart
- Quantity tracking per item
- Search and filter items in cart
- Total price calculation
- Cart count shown in header

### Other

- State management with **Pinia**
- Fully responsive layout
- Clean project structure for scalability

---

## 🗂 Project Structure

src/
├── assets/ # Static assets like images, CSS
├── components/ # Reusable Vue components (ProductCard.vue)
├── data/ # Mock data (products.js)
├── layouts/ # Layouts (MainLayout.vue)
├── stores/ # Pinia stores (cart.js)
├── views/ # Pages (ProductsView, ProductDetailView, CartView)
├── router/ # Vue Router setup (index.js)
└── main.js # Entry point

---

## ⚡ Technologies

- Vue 3 + Vite
- Vue Router
- Pinia (state management)
- TailwindCSS
- JavaScript (ES6+)

---

## 🚀 Installation

Clone the repo:

```bash
git clone <your-repo-url>
cd vue-shop


npm install

npm run dev




💡 Notes

Mock data is located in src/data/products.js

Cart state persists during runtime (can extend to localStorage)

Filtering & search are reactive using computed properties

Layout is responsive and clean with TailwindCSS


📦 Commit Guidelines (used in this project)

feat: feature added

refactor: code refactored

chore: setup / config changes
