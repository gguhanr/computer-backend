
# Sen Kumaran Info Tech 🖥️  

A full-stack website for **Sen Kumaran Info Tech**, a computer sales & service shop. Customers can browse products, add them to a cart, and place orders or book repair services straight to WhatsApp. The shop owner manages everything from a secure admin panel.

**Live site:** https://senkumaraninfotech.netlify.app

---

## ✨ Features

### Customer storefront (`index.html`)
- Products loaded live from MongoDB
- Filter products by category (type)
- Stock badges: In Stock / Low Stock / Out of Stock
- Cart with quantity controls and running total
- Checkout → order saved to database → opens WhatsApp with the full order details
- Service booking form (repairs, CCTV, etc.) → saved to database + sent via WhatsApp
- Responsive design with animations (Tailwind CSS)

### Admin panel (`admin.html`)
- Secure login with JWT
- Dashboard: total products, out-of-stock count, new service requests, pending orders, products per category
- Products: add, edit, delete, hide/show, quick-change category
- Service requests: filter by status and update (New → In Progress → Completed / Cancelled)
- Orders: view items and totals, update status (Pending → Confirmed → Fulfilled / Cancelled)

---

## 🛠️ Tech Stack

| Part | Technology |
|------|------------|
| Frontend | HTML, Tailwind CSS, Vanilla JavaScript, Font Awesome |
| Backend | Node.js, Express |
| Database | MongoDB (Atlas) |
| Auth | JSON Web Tokens (JWT) |
| Hosting | Netlify (frontend), Render (backend) |

---

## 📁 Project Structure

```
├── index.html     # Customer storefront
├── main.js        # Storefront logic: products, cart, checkout, bookings
├── admin.html     # Admin panel UI
├── admin.js       # Admin logic: login, dashboard, CRUD
└── README.md
```

> The backend (Express + MongoDB) lives in its own repository / folder and is deployed on Render.

---

## 🔌 API Endpoints



| Method | Endpoint | Access | Description |
|--------|----------|--------|-------------|
| GET | `/products` | Public | List active products |
| GET | `/products?all=1` | Admin | List all products (incl. hidden) |
| POST | `/products` | Admin | Create product |
| PUT | `/products/:id` | Admin | Update product |
| PATCH | `/products/:id/type` | Admin | Change product category |
| DELETE | `/products/:id` | Admin | Delete product |
| POST | `/orders` | Public | Place an order |
| GET | `/orders` | Admin | List orders |
| PATCH | `/orders/:id` | Admin | Update order status |
| POST | `/service-requests` | Public | Submit a service booking |
| GET | `/service-requests?status=` | Admin | List service requests |
| PATCH | `/service-requests/:id` | Admin | Update request status |
| DELETE | `/service-requests/:id` | Admin | Delete request |
| POST | `/auth/login` | Public | Admin login → returns JWT |
| GET | `/auth/me` | Admin | Current admin info |
| GET | `/dashboard/stats` | Admin | Dashboard statistics |

Admin routes need the header `Authorization: Bearer <token>`.

---

## 🚀 Getting Started

### 1. Clone
```bash
git clone https://github.com/<your-username>/<repo-name>.git
cd <repo-name>
```

## 🌐 Deployment

**Backend → Render**
1. Push the backend to GitHub and create a new *Web Service* on Render.
2. Add `MONGO_URI`, `JWT_SECRET`, `WHATSAPP_NUMBER` under **Environment**.
3. In MongoDB Atlas → **Network Access**, allow `0.0.0.0/0`.

**Frontend → Netlify**
1. Drag the project folder onto [app.netlify.com/drop](https://app.netlify.com/drop), or connect this repo.
2. Make sure `API_BASE` in `main.js` and `admin.js` uses the Render URL ending in `/api`.

> ⏳ Render's free tier sleeps after ~15 minutes of inactivity. The first request can take 30–60 seconds; the storefront retries automatically while the server wakes up.

---

## 🧯 Troubleshooting

| Problem | Cause | Fix |
|---------|-------|-----|
| "Could not load products right now." | Wrong `API_BASE` or server asleep | Check the URL ends in `/api`; wait a minute and refresh |
| Console: *violates Content Security Policy "connect-src"* | Host blocks outside connections | Add the API domain to `connect-src`, or host on Netlify |
| Console: *blocked by CORS policy* | Backend not allowing the frontend domain | Add `app.use(cors())` in `server.js` |
| 404 on API calls | Missing `/api` in `API_BASE` | Use `.../api` as the base URL |
| 500 errors | MongoDB not connected | Check `MONGO_URI` and Atlas network access; see Render logs |

---

## 📞 Contact

**Sen Kumaran Info Tech**
WhatsApp: +91 XXXXX XXXXX

---

## 📄 License

This project is for Sen Kumaran Info Tech. All rights reserved.
