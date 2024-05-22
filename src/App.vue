<template>
  <q-layout view="hHh lpR fFf">
    <q-header elevated class="bg-primary text-white" height-hint="98">
      <q-toolbar>
        <q-btn dense flat round icon="menu" @click="toggleLeftDrawer" />

        <q-toolbar-title>
          <q-avatar>
            <img src="../src/assets/logo-smartphone-store.png" />
          </q-avatar>
          Smartphone Store
        </q-toolbar-title>
      </q-toolbar>

      <q-tabs align="left">
        <q-route-tab to="/page1" label="Smartphone Shop" />
        <q-route-tab to="/page2" label="Accessories Shop" />
      </q-tabs>
    </q-header>

    <q-drawer
      show-if-above
      v-model="leftDrawerOpen"
      side="left"
      bordered
      class="drawer-style"
    >
      <!-- Menu card content -->
      <q-card class="q-mt-md">
        <q-card-section>
          <div class="menu-title">Menu</div>
        </q-card-section>

        <q-list>
          <!-- Menu Item 1 -->
          <q-item clickable v-ripple class="menu-item">
            <q-item-section avatar class="menu-item-icon">
              <q-icon name="home" />
            </q-item-section>
            <q-item-section class="menu-item-text"> Home </q-item-section>
          </q-item>

          <!-- Menu Item 2 -->
          <q-item clickable v-ripple class="menu-item">
            <q-item-section avatar class="menu-item-icon">
              <q-icon name="smartphone" />
            </q-item-section>
            <q-item-section class="menu-item-text">
              Smartphones
            </q-item-section>
          </q-item>

          <!-- Menu Item 3 -->
          <q-item clickable v-ripple class="menu-item">
            <q-item-section avatar class="menu-item-icon">
              <q-icon name="star" />
            </q-item-section>
            <q-item-section class="menu-item-text"> Offers </q-item-section>
          </q-item>

          <!-- Menu Item 4 -->
          <q-item clickable v-ripple class="menu-item">
            <q-item-section avatar class="menu-item-icon">
              <q-icon name="info" />
            </q-item-section>
            <q-item-section class="menu-item-text"> About Us </q-item-section>
          </q-item>
        </q-list>
      </q-card>

      <!-- Submenu at the bottom -->
      <q-card class="q-mt-md">
        <q-card-section>
          <div class="menu-title">Settings</div>
        </q-card-section>
        <q-list>
          <q-item class="submenu-item" clickable v-ripple>
            <q-item-section avatar class="menu-item-icon">
              <q-icon name="person" />
            </q-item-section>
            <q-item-section class="submenu-item-text"> Profile </q-item-section>
          </q-item>
          <q-item class="submenu-item" clickable v-ripple>
            <q-item-section avatar class="menu-item-icon">
              <q-icon name="tune" />
            </q-item-section>
            <q-item-section class="submenu-item-text">
              Preferences
            </q-item-section>
          </q-item>
          <q-item class="submenu-item" clickable v-ripple>
            <q-item-section avatar class="menu-item-icon">
              <q-icon name="security" />
            </q-item-section>
            <q-item-section class="submenu-item-text">
              Security
            </q-item-section>
          </q-item>
        </q-list>
      </q-card>
    </q-drawer>

    <q-page-container class="container-style">
      <router-view />
      <div class="q-pa-md">
        <!-- Display Carousel Slides -->
        <div class="q-gutter-md">
          <q-img src="./assets/background-carousel1.png" class="carousel-style">
            <div class="absolute-bottom custom-caption">
              <div class="text-h2">Latest Smartphones</div>
              <div class="text-subtitle1">Discover Now</div>
            </div>
          </q-img>
          <q-img src="./assets/background-carousel2.png" class="carousel-style">
            <div class="absolute-bottom custom-caption">
              <div class="text-h2">Top Brands</div>
              <div class="text-subtitle1">Best Prices</div>
            </div>
          </q-img>
          <q-img src="./assets/background-carousel3.png" class="carousel-style">
            <div class="absolute-bottom custom-caption">
              <div class="text-h2">Exclusive Offers</div>
              <div class="text-subtitle1">Shop Now</div>
            </div>
          </q-img>
        </div>

        <!-- Product Section -->
        <div class="product-section">
          <q-banner class="q-my-md">
            <template v-slot:avatar>
              <q-icon name="star" />
            </template>
            Special Discount on New Arrivals!
          </q-banner>

          <div class="q-gutter-md">
            <q-card
              class="my-card"
              v-for="product in products"
              :key="product.id"
            >
              <q-img
                :src="product.image"
                :alt="product.name"
                class="product-image"
                contain
              />
              <q-card-section>
                <div class="product-title">{{ product.name }}</div>
                <div class="product-description">{{ product.description }}</div>
              </q-card-section>
              <q-card-actions align="right">
                <q-btn flat label="Details" @click="viewDetails(product.id)" />
                <q-btn
                  flat
                  label="Add to Cart"
                  color="primary"
                  @click="addToCart(product)"
                />
              </q-card-actions>
            </q-card>
          </div>
        </div>
      </div>
    </q-page-container>

    <q-footer elevated class="bg-grey-8 text-white">
      <q-toolbar class="background-footer">
        <q-toolbar-title>
          <q-avatar>
            <img src="../src/assets/logo-smartphone-store.png" />
          </q-avatar>
          Smartphone Store
        </q-toolbar-title>
        <div class="footer-content">
          <div class="footer-section">
            <div class="footer-title">Contact Us</div>
            <div class="footer-item">
              <q-icon name="person" class="footer-icon" />
              <span>Reza Ibnu Hanifa</span>
            </div>
            <div class="footer-item">
              <q-icon name="email" class="footer-icon" />
              <span>rezaibnu752@gmail.com</span>
            </div>
            <div class="footer-item">
              <q-icon name="whatsapp" class="footer-icon" />
              <span>+62895620310374</span>
            </div>
          </div>
        </div>
      </q-toolbar>
    </q-footer>

    <!-- Checkout Modal -->
    <q-dialog v-model="checkoutDialog">
      <q-card>
        <q-card-section>
          <div class="text-h6">Checkout</div>
        </q-card-section>

        <q-card-section>
          <div v-for="item in cart" :key="item.id">
            <div>{{ item.name }} - {{ item.description }}</div>
          </div>
        </q-card-section>

        <q-card-actions align="right">
          <q-btn
            flat
            label="Close"
            color="primary"
            @click="checkoutDialog = false"
          />
          <q-btn
            flat
            label="Proceed to Payment"
            color="primary"
            @click="proceedToPayment"
          />
        </q-card-actions>
      </q-card>
    </q-dialog>
  </q-layout>
</template>

<script>
import { ref } from "vue";

export default {
  setup() {
    const leftDrawerOpen = ref(false);
    const slide = ref("first");
    const checkoutDialog = ref(false);
    const cart = ref([]);

    const products = ref([
      {
        id: 1,
        name: "iPhone 13",
        description: "Latest Apple smartphone with A15 Bionic chip",
        image: "./src/assets/iphone13.png",
      },
      {
        id: 2,
        name: "Samsung Galaxy S21",
        description: "High-end Android phone with excellent camera",
        image: "./src/assets/galaxys21.png",
      },
      {
        id: 3,
        name: "Google Pixel 6",
        description: "Smartphone with pure Android experience",
        image: "./src/assets/pixel6.png",
      },
      {
        id: 4,
        name: "OnePlus 9 Pro",
        description: "Flagship killer with top-notch specs",
        image: "./src/assets/oneplus9pro.png",
      },
      {
        id: 5,
        name: "Xiaomi 14",
        description: "Affordable phone with flagship features",
        image: "./src/assets/mi14.png",
      },
      {
        id: 6,
        name: "Sony Xperia 1 III",
        description: "Phone with 4K display and great multimedia features",
        image: "./src/assets/xperia1iii.png",
      },
      {
        id: 7,
        name: "Huawei P40 Pro",
        description: "Phone with powerful camera and hardware",
        image: "./src/assets/p40pro.png",
      },
      {
        id: 8,
        name: "Oppo Find X3 Pro",
        description: "Phone with excellent design and performance",
        image: "./src/assets/findx3pro.png",
      },
      {
        id: 9,
        name: "Motorola Edge+",
        description: "Phone with curved display and flagship specs",
        image: "./src/assets/edgeplus.png",
      },
      {
        id: 10,
        name: "Asus ROG Phone 5",
        description: "Gaming phone with top-tier performance",
        image: "./src/assets/rogphone5.png",
      },
      {
        id: 11,
        name: "Realme GT Master",
        description: "Affordable performance phone",
        image: "./src/assets/realmegt.png",
      },
    ]);

    const viewDetails = (id) => {
      console.log("View details for product", id);
    };

    const addToCart = (product) => {
      cart.value.push(product);
      checkoutDialog.value = true;
    };

    const proceedToPayment = () => {
      console.log("Proceed to payment with items", cart.value);
      checkoutDialog.value = false;
    };

    return {
      leftDrawerOpen,
      toggleLeftDrawer() {
        leftDrawerOpen.value = !leftDrawerOpen.value;
      },
      slide,
      products,
      viewDetails,
      addToCart,
      checkoutDialog,
      cart,
      proceedToPayment,
    };
  },
};
</script>

<style scoped>
.custom-caption {
  text-align: center;
  padding: 12px;
  color: white;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
}

.bg-primary {
  background-color: black !important;
}

.container-style {
  padding: 16px;
  background-color: #f5f5f5;
}

.carousel-style {
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
}

.drawer-style {
  background-color: #f0f0f0;
  padding: 16px;
}

.q-carousel-slide img {
  object-fit: cover;
  transition: transform 0.5s ease;
}

.q-carousel-slide img:hover {
  transform: scale(1.05);
}

.product-section {
  margin-top: 32px;
}

.my-card {
  width: 300px;
  margin: 16px;
  display: inline-block;
  vertical-align: top;
}

.product-image {
  width: 100%;
  height: 300px;
  object-fit: contain;
}

.q-banner {
  background-color: #ffeb3b !important;
  color: #000;
  border-radius: 8px;
}

.product-title {
  font-size: 18px;
  font-weight: bold;
  margin-top: 8px;
}

.product-description {
  font-size: 14px;
  margin-top: 8px;
}

.btn {
  display: inline-block;
  padding: 10px 20px;
  background-color: #1a73e8;
  color: #fff;
  text-decoration: none;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.btn:hover {
  background-color: #0c54c9;
}

.bg-grey-8 {
  background-color: #303030 !important;
}

.text-white {
  color: #fff !important;
}

.drawer-style {
  background-color: #ffffff;
  padding: 16px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

.q-mt-md {
  margin-top: 16px;
}

.menu-title {
  font-size: 18px;
  font-weight: bold;
  color: #333;
}

.menu-item {
  display: flex;
  align-items: center;
  padding: 12px 16px;
  border-bottom: 1px solid #e0e0e0;
  transition: background-color 0.3s;
}

.menu-item:hover {
  background-color: #f9f9f9;
}

.menu-item-icon {
  margin-right: 12px;
  color: black;
}

.menu-item-text {
  font-size: 16px;
  color: #555;
}

.submenu {
  margin-left: 24px;
}

.submenu-item {
  display: flex;
  align-items: center;
  padding: 8px 16px;
  transition: background-color 0.3s;
}

.submenu-item:hover {
  background-color: #f9f9f9;
}

.submenu-item-text {
  font-size: 14px;
  color: #555;
}

.footer-content {
  display: flex;
  flex-direction: column;
  align-items: flex-end; 
  margin-left: auto; 
}

.footer-section {
  display: flex;
  flex-direction: column;
  align-items: flex-end;
}

.footer-title {
  font-size: 18px;
  font-weight: bold;
  margin-bottom: 8px;
  color: #ffffff;
}

.footer-item {
  display: flex;
  align-items: center;
  margin-bottom: 4px;
  color: #ffffff;
}

.footer-icon {
  margin-right: 8px;
  color: #ffeb3b;
}

.background-footer {
  background-color: black;
}
</style>
