<template lang="">
    
<aside id="layout-menu" class="layout-menu menu-vertical menu bg-menu-theme" style="background-color: var(--bs-gray-60);">
  
  <div class="app-brand demo ">
    <a href="" class="app-brand-link ">
      <span class="app-brand-logo demo">
<span class="text-primary">

  
</span>
</span>
      <span>
        <span class="app-brand-text demo menu-text fw-semibold ms-2">ລະບົບ POS</span>
      </span>
      <img src="/public/assets/img/cashier.png" class="w-25 " alt="Logo">
    </a>

    <!-- <a href="javascript:void(0);" class="layout-menu-toggle menu-link text-large ms-auto">
      <i class="bx bx-chevron-left d-block d-xl-none align-middle"></i>
    </a> -->
  </div>

  
  <div class="menu-divider mt-2"></div>

  <div class="menu-inner-shadow"></div>

  

  <ul class="menu-inner py-1">
  
      <li class="menu-item mb-1" v-for="item in menuItems" :key="item.name" :class="{'active': item.active}" > 
        <router-link :to="item.link" class="menu-link d-flex align-items-center text-dark text-decoration-none px-3 py-2 rounded hover-bg-light">
          <i :class="['menu-icon', 'bx', item.icon, 'me-3', 'fs-5']"></i>
          <div class="text-truncate fw-semibold">{{ item.label }}</div>
        </router-link>
      </li>

  </ul>
</aside>
</template>
<script>
export default {
    data() {
        return {
            menuItems: [
                { 
                    name: "store", 
                    label: "ສະຕ໋ອກ", 
                    icon: "bxs-store",
                    link: "/store",
                    active: false,
                },
                { 
                    name: "category", 
                    label: "ໝວດໝູ່", 
                    icon: "bxs-category",
                    link: "/category",
                    active: false,
                },
                { 
                    name: "pos", 
                    label: "POS", 
                    icon: "bxs-cart-alt",
                    link: "/pos",
                    active: false,
                },
                { 
                    name: "activity", 
                    label: "ການເຄື່ອນໄຫວ", 
                    icon: "bxs-bar-chart-alt-2",
                    link: "/transection",
                    active: false,
                },
                { 
                    name: "report", 
                    label: "ລາຍງານ", 
                    icon: "bxs-receipt",
                    link: "/report",
                    active: false,
                  },
            ],
        }
    },
    watch: {
        $route(to, from) {
            this.updateActiveMenuItem();
        }
    },

  methods: {
        updateActiveMenuItem() {
          this.menuItems.forEach(item => {
              item.active = (item.link === this.$route.path);
            });
        }
  }
}

</script>
<style lang="">
    
</style>