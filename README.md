## Online-grocery website
using bootstrap,React.js,Postam,mongo

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>FoodExpress | Order Your Favorite Food Anytime</title>
<meta name="description" content="FoodExpress - premium food delivery from your favorite restaurants, delivered fast.">

<!-- Google Fonts -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@500;600;700;800;900&family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">

<!-- Bootstrap 5 CSS -->
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet">
<!-- Bootstrap Icons -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.11.3/font/bootstrap-icons.css">
<!-- Custom CSS -->
<link rel="stylesheet" href="style.css">
</head>
<body>

<!-- ===================== LOADING SCREEN ===================== -->
<div id="loader" class="loader-screen">
  <div class="loader-plate">
    <div class="loader-ring"></div>
    <i class="bi bi-egg-fried loader-icon"></i>
  </div>
  <p class="loader-text">FoodExpress</p>
</div>

<!-- ===================== NAVBAR ===================== -->
<nav class="navbar navbar-expand-lg fixed-top" id="mainNavbar">
  <div class="container">
    <a class="navbar-brand" href="#home">
      <i class="bi bi-egg-fried"></i> Food<span>Express</span>
    </a>
    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navMenu" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>

    <div class="collapse navbar-collapse" id="navMenu">
      <ul class="navbar-nav mx-auto align-items-lg-center gap-lg-1">
        <li class="nav-item"><a class="nav-link active" href="#home">Home</a></li>
        <li class="nav-item"><a class="nav-link" href="#restaurants">Restaurants</a></li>
        <li class="nav-item"><a class="nav-link" href="#menu">Menu</a></li>
        <li class="nav-item"><a class="nav-link" href="#offers">Offers</a></li>
        <li class="nav-item"><a class="nav-link" href="#contact">Contact</a></li>
      </ul>

      <form class="d-flex nav-search me-lg-3 my-3 my-lg-0" role="search" onsubmit="return false;">
        <i class="bi bi-search"></i>
        <input class="form-control" type="search" id="navSearchInput" placeholder="Search food, restaurant, cuisine...">
      </form>

      <div class="d-flex align-items-center gap-2">
        <button class="btn btn-outline-nav" data-bs-toggle="modal" data-bs-target="#loginModal">
          <i class="bi bi-person"></i> Login
        </button>
        <button class="btn btn-cart-toggle position-relative" data-bs-toggle="offcanvas" data-bs-target="#cartCanvas" aria-label="Open cart">
          <i class="bi bi-basket3"></i>
          <span class="badge cart-count" id="navCartCount">0</span>
        </button>
      </div>
    </div>
  </div>
</nav>

<!-- ===================== HERO SECTION ===================== -->
<header class="hero-section" id="home">
  <div class="hero-overlay"></div>
  <div class="container position-relative">
    <div class="row align-items-center min-vh-100 py-5">
      <div class="col-lg-7 hero-text" data-aos>
        <span class="hero-eyebrow"><i class="bi bi-lightning-charge-fill"></i> Delivering happiness, hot & fresh</span>
        <h1 class="hero-heading">Order Your Favorite Food <span class="text-gradient">Anytime</span></h1>
        <p class="hero-desc">
          From sizzling street food to fine dining, FoodExpress brings 200+ restaurants
          to your doorstep in under 30 minutes. Real-time tracking, real good food.
        </p>
        <div class="hero-btns">
          <a href="#menu" class="btn btn-hero-primary">Order Now <i class="bi bi-arrow-right"></i></a>
          <a href="#menu" class="btn btn-hero-outline">Explore Menu</a>
        </div>
        <div class="hero-stats">
          <div><strong>200+</strong><span>Restaurants</span></div>
          <div><strong>50k+</strong><span>Orders Delivered</span></div>
          <div><strong>4.8</strong><span>Avg. Rating</span></div>
        </div>
      </div>
    </div>
  </div>
  <div class="hero-scroll-cue"><i class="bi bi-chevron-down"></i></div>
</header>

<!-- ===================== RESTAURANTS SECTION ===================== -->
<section class="section-padding" id="restaurants">
  <div class="container">
    <div class="section-heading">
      <span class="eyebrow">01 &mdash; Where to order from</span>
      <h2>Popular Restaurants</h2>
      <p>Hand-picked kitchens our riders love visiting the most.</p>
    </div>

    <div class="row g-4" id="restaurantGrid"></div>
  </div>
</section>

<!-- ===================== MENU SECTION ===================== -->
<section class="section-padding bg-soft" id="menu">
  <div class="container">
    <div class="section-heading">
      <span class="eyebrow">02 &mdash; Pick your cravings</span>
      <h2>Our Food Menu</h2>
      <p>Filter, search, and add your favorites to the cart in seconds.</p>
    </div>

    <!-- Filters -->
    <div class="filter-bar">
      <div class="filter-group">
        <label class="filter-label">Category</label>
        <div class="btn-group flex-wrap" role="group" id="categoryFilter">
          <button class="filter-chip active" data-filter="category" data-value="all">All</button>
          <button class="filter-chip" data-filter="category" data-value="veg">Veg</button>
          <button class="filter-chip" data-filter="category" data-value="non-veg">Non-Veg</button>
        </div>
      </div>

      <div class="filter-group">
        <label class="filter-label">Cuisine</label>
        <select class="form-select filter-select" id="cuisineFilter">
          <option value="all">All Cuisines</option>
          <option value="Indian">Indian</option>
          <option value="Chinese">Chinese</option>
          <option value="Italian">Italian</option>
          <option value="Fast Food">Fast Food</option>
          <option value="South Indian">South Indian</option>
          <option value="Desserts">Desserts</option>
        </select>
      </div>

      <div class="filter-group">
        <label class="filter-label">Price</label>
        <select class="form-select filter-select" id="priceFilter">
          <option value="all">Any Price</option>
          <option value="under200">Under ₹200</option>
          <option value="200to500">₹200 &ndash; ₹500</option>
          <option value="above500">Above ₹500</option>
        </select>
      </div>

      <div class="filter-group flex-grow-1">
        <label class="filter-label">Search</label>
        <div class="menu-search">
          <i class="bi bi-search"></i>
          <input type="search" id="menuSearchInput" class="form-control" placeholder="Search dishes, restaurants, cuisines...">
        </div>
      </div>
    </div>

    <div class="row g-4" id="menuGrid"></div>
    <p class="text-center no-results d-none" id="noResults">
      <i class="bi bi-emoji-frown"></i> No dishes match your filters. Try clearing a few.
    </p>
  </div>
</section>

<!-- ===================== OFFERS CAROUSEL ===================== -->
<section class="section-padding" id="offers">
  <div class="container">
    <div class="section-heading">
      <span class="eyebrow">03 &mdash; Deals worth craving</span>
      <h2>This Week's Offers</h2>
    </div>

    <div id="offersCarousel" class="carousel slide offer-carousel" data-bs-ride="carousel">
      <div class="carousel-indicators">
        <button type="button" data-bs-target="#offersCarousel" data-bs-slide-to="0" class="active"></button>
        <button type="button" data-bs-target="#offersCarousel" data-bs-slide-to="1"></button>
        <button type="button" data-bs-target="#offersCarousel" data-bs-slide-to="2"></button>
        <button type="button" data-bs-target="#offersCarousel" data-bs-slide-to="3"></button>
        <button type="button" data-bs-target="#offersCarousel" data-bs-slide-to="4"></button>
      </div>
      <div class="carousel-inner" id="offerCarouselInner"></div>
      <button class="carousel-control-prev" type="button" data-bs-target="#offersCarousel" data-bs-slide="prev">
        <span class="carousel-control-prev-icon"></span>
      </button>
      <button class="carousel-control-next" type="button" data-bs-target="#offersCarousel" data-bs-slide="next">
        <span class="carousel-control-next-icon"></span>
      </button>
    </div>
  </div>
</section>

<!-- ===================== FAQ SECTION ===================== -->
<section class="section-padding bg-soft" id="faq">
  <div class="container">
    <div class="section-heading">
      <span class="eyebrow">04 &mdash; Good to know</span>
      <h2>Frequently Asked Questions</h2>
    </div>
    <div class="accordion faq-accordion" id="faqAccordion">
      <div class="accordion-item">
        <h2 class="accordion-header">
          <button class="accordion-button" type="button" data-bs-toggle="collapse" data-bs-target="#faq1">
            How fast is delivery?
          </button>
        </h2>
        <div id="faq1" class="accordion-collapse collapse show" data-bs-parent="#faqAccordion">
          <div class="accordion-body">Most orders arrive within 25&ndash;40 minutes depending on your distance from the restaurant and live traffic conditions.</div>
        </div>
      </div>
      <div class="accordion-item">
        <h2 class="accordion-header">
          <button class="accordion-button collapsed" type="button" data-bs-toggle="collapse" data-bs-target="#faq2">
            Can I pay cash on delivery?
          </button>
        </h2>
        <div id="faq2" class="accordion-collapse collapse" data-bs-parent="#faqAccordion">
          <div class="accordion-body">Yes. At checkout choose "Cash on Delivery" alongside cards, UPI, and wallets.</div>
        </div>
      </div>
      <div class="accordion-item">
        <h2 class="accordion-header">
          <button class="accordion-button collapsed" type="button" data-bs-toggle="collapse" data-bs-target="#faq3">
            How do I track my order?
          </button>
        </h2>
        <div id="faq3" class="accordion-collapse collapse" data-bs-parent="#faqAccordion">
          <div class="accordion-body">Once confirmed, a live tracking link is generated so you can watch your rider on the map in real time.</div>
        </div>
      </div>
      <div class="accordion-item">
        <h2 class="accordion-header">
          <button class="accordion-button collapsed" type="button" data-bs-toggle="collapse" data-bs-target="#faq4">
            What if an item is missing?
          </button>
        </h2>
        <div id="faq4" class="accordion-collapse collapse" data-bs-parent="#faqAccordion">
          <div class="accordion-body">Contact support within 24 hours from the Orders page and we'll refund or resend the missing item.</div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- ===================== CONTACT SECTION ===================== -->
<section class="section-padding" id="contact">
  <div class="container">
    <div class="section-heading">
      <span class="eyebrow">05 &mdash; Talk to us</span>
      <h2>Get in Touch</h2>
    </div>

    <div class="row g-4">
      <div class="col-lg-6">
        <form class="contact-form" id="contactForm" novalidate>
          <div class="row g-3">
            <div class="col-md-6">
              <label class="form-label">Name</label>
              <input type="text" class="form-control" id="contactName" required>
              <div class="invalid-feedback">Please enter your name.</div>
            </div>
            <div class="col-md-6">
              <label class="form-label">Email</label>
              <input type="email" class="form-control" id="contactEmail" required>
              <div class="invalid-feedback">Please enter a valid email.</div>
            </div>
            <div class="col-md-6">
              <label class="form-label">Phone</label>
              <input type="tel" class="form-control" id="contactPhone" required pattern="[0-9]{10}">
              <div class="invalid-feedback">Please enter a 10-digit phone number.</div>
            </div>
            <div class="col-md-6">
              <label class="form-label">Subject</label>
              <input type="text" class="form-control" id="contactSubject" placeholder="Optional">
            </div>
            <div class="col-12">
              <label class="form-label">Message</label>
              <textarea class="form-control" id="contactMessage" rows="4" required></textarea>
              <div class="invalid-feedback">Please write a short message.</div>
            </div>
            <div class="col-12">
              <button type="submit" class="btn btn-hero-primary w-100">Send Message</button>
            </div>
          </div>
        </form>
      </div>

      <div class="col-lg-6">
        <div class="contact-info-card">
          <div class="map-placeholder">
            <i class="bi bi-geo-alt-fill"></i>
            <span>Map preview</span>
          </div>
          <ul class="contact-details">
            <li><i class="bi bi-geo-alt"></i> 221B Spice Street, Connaught Place, New Delhi</li>
            <li><i class="bi bi-envelope"></i> hello@foodexpress.example</li>
            <li><i class="bi bi-telephone"></i> +91 98765 43210</li>
          </ul>
          <div class="social-icons">
            <a href="#" aria-label="Facebook"><i class="bi bi-facebook"></i></a>
            <a href="#" aria-label="Instagram"><i class="bi bi-instagram"></i></a>
            <a href="#" aria-label="Twitter"><i class="bi bi-twitter-x"></i></a>
            <a href="#" aria-label="YouTube"><i class="bi bi-youtube"></i></a>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- ===================== FOOTER ===================== -->
<footer class="site-footer">
  <div class="container">
    <div class="row g-4">
      <div class="col-lg-4">
        <a class="footer-brand" href="#home"><i class="bi bi-egg-fried"></i> Food<span>Express</span></a>
        <p class="footer-tagline">Premium food delivery, from kitchen to doorstep &mdash; fast, fresh, and always on time.</p>
        <div class="social-icons">
          <a href="#" aria-label="Facebook"><i class="bi bi-facebook"></i></a>
          <a href="#" aria-label="Instagram"><i class="bi bi-instagram"></i></a>
          <a href="#" aria-label="Twitter"><i class="bi bi-twitter-x"></i></a>
          <a href="#" aria-label="YouTube"><i class="bi bi-youtube"></i></a>
        </div>
      </div>

      <div class="col-lg-2 col-6">
        <h6>Quick Links</h6>
        <ul class="footer-links">
          <li><a href="#home">Home</a></li>
          <li><a href="#restaurants">Restaurants</a></li>
          <li><a href="#menu">Menu</a></li>
          <li><a href="#offers">Offers</a></li>
          <li><a href="#contact">Contact</a></li>
        </ul>
      </div>

      <div class="col-lg-3 col-6">
        <h6>Contact</h6>
        <ul class="footer-links">
          <li><i class="bi bi-geo-alt"></i> New Delhi, India</li>
          <li><i class="bi bi-envelope"></i> hello@foodexpress.example</li>
          <li><i class="bi bi-telephone"></i> +91 98765 43210</li>
        </ul>
      </div>

      <div class="col-lg-3">
        <h6>Newsletter</h6>
        <p class="footer-links-p">Get offers straight to your inbox.</p>
        <form class="newsletter-form" id="newsletterForm" onsubmit="return false;">
          <input type="email" class="form-control" placeholder="Your email" required>
          <button class="btn btn-hero-primary" type="submit"><i class="bi bi-send"></i></button>
        </form>
      </div>
    </div>

    <hr>
    <p class="copyright">&copy; 2026 FoodExpress. All rights reserved.</p>
  </div>
</footer>

<!-- ===================== FOOD DETAILS MODAL ===================== -->
<div class="modal fade" id="foodDetailsModal" tabindex="-1" aria-hidden="true">
  <div class="modal-dialog modal-dialog-centered modal-lg">
    <div class="modal-content" id="foodModalContent">
      <!-- populated by JS -->
    </div>
  </div>
</div>

<!-- ===================== LOGIN MODAL ===================== -->
<div class="modal fade" id="loginModal" tabindex="-1" aria-hidden="true">
  <div class="modal-dialog modal-dialog-centered">
    <div class="modal-content">
      <div class="modal-header border-0">
        <h5 class="modal-title">Welcome back</h5>
        <button type="button" class="btn-close" data-bs-dismiss="modal"></button>
      </div>
      <div class="modal-body">
        <form id="loginForm">
          <div class="mb-3">
            <label class="form-label">Email or Phone</label>
            <input type="text" class="form-control" required>
          </div>
          <div class="mb-3">
            <label class="form-label">Password</label>
            <input type="password" class="form-control" required>
          </div>
          <button type="submit" class="btn btn-hero-primary w-100">Login</button>
        </form>
      </div>
    </div>
  </div>
</div>

<!-- ===================== CART OFFCANVAS ===================== -->
<div class="offcanvas offcanvas-end cart-offcanvas" tabindex="-1" id="cartCanvas">
  <div class="offcanvas-header">
    <h5 class="offcanvas-title"><i class="bi bi-basket3"></i> Your Cart</h5>
    <button type="button" class="btn-close" data-bs-dismiss="offcanvas"></button>
  </div>
  <div class="offcanvas-body d-flex flex-column">
    <div id="cartItemsContainer" class="cart-items-container flex-grow-1"></div>

    <div class="cart-empty-state d-none" id="cartEmptyState">
      <i class="bi bi-basket2"></i>
      <p>Your cart is empty. Go add something delicious!</p>
    </div>

    <div class="cart-summary" id="cartSummary">
      <div class="d-flex justify-content-between">
        <span>Subtotal</span>
        <span id="cartSubtotal">₹0</span>
      </div>
      <div class="d-flex justify-content-between">
        <span>Delivery Fee</span>
        <span id="cartDelivery">₹0</span>
      </div>
      <div class="d-flex justify-content-between fw-bold cart-total-row">
        <span>Total</span>
        <span id="cartTotal">₹0</span>
      </div>
      <div class="d-flex gap-2 mt-3">
        <button class="btn btn-outline-nav flex-fill" id="emptyCartBtn">Empty Cart</button>
        <button class="btn btn-hero-primary flex-fill" id="checkoutBtn">Checkout</button>
      </div>
    </div>
  </div>
</div>

<!-- ===================== TOAST CONTAINER ===================== -->
<div class="toast-container position-fixed bottom-0 end-0 p-3" id="toastContainer"></div>

<!-- ===================== SCROLL TO TOP ===================== -->
<button id="scrollTopBtn" aria-label="Scroll to top"><i class="bi bi-arrow-up"></i></button>

<!-- Bootstrap JS Bundle -->
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js"></script>
<!-- Custom JS -->
<script src="script.js"></script>
</body>
</html>
SCREENSHOT
<img width="1600" height="881" alt="image" src="https://github.com/user-attachments/assets/0cb9cd12-9349-4e3f-85f4-c8251f7e1836" />
<img width="1600" height="882" alt="image" src="https://github.com/user-attachments/assets/4fdb2ecb-6b2a-4e5e-8fcc-1eccd31d4881" />



##Outcome of Grocery App
* Developed a user-friendly Online Grocery
*  Delivery Application for browsing and purchasing grocery products.
* Implemented product listing, product management, and order-related functionality.
* Created a responsive frontend for a smooth user experience.
* Developed REST APIs using Node.js and Express.js.
* Integrated MongoDB for storing and managing product and user data.
* Improved understanding of full-stack development, API integration, database management, and authentication.
* The application provides a convenient way for users to view groceries and place orders online. View all details of past or present history order
* To do shopping all things 
