<template lang="">
    
   
    <!-- Layout wrapper -->
<div class="layout-wrapper layout-content-navbar  ">
  <div class="layout-container">
    
    




<!-- Menu -->
     <!-- Check: {{ authStore.isAuthenticated }} -->
   <sidebar v-if="authStore.isAuthenticated"></sidebar>

<!-- / Menu -->

    

    <!-- Layout container -->
    <div class="layout-page">
      
      



<!-- Navbar -->

<nav v-if="authStore.isAuthenticated" class="layout-navbar container-xxl navbar-detached navbar navbar-expand-xl align-items-center bg-navbar-theme" id="layout-navbar">
  




  <div class="layout-menu-toggle navbar-nav align-items-xl-center me-4 me-xl-0   d-xl-none ">
    <a class="nav-item nav-link px-0 me-xl-6" href="javascript:void(0)">
      <i class="icon-base bx bx-menu icon-md"></i>
    </a>
  </div>


<div class="navbar-nav-right d-flex align-items-center justify-content-end" id="navbar-collapse">
  
  

  
    <!-- Search -->
     
    <!-- /Search -->
  

  <ul class="navbar-nav flex-row align-items-center ms-md-auto">
    
      
        <!-- Place this tag where you want the button to render. -->
        <li class="nav-item lh-1 me-4">
          <a class="github-button" href="https://github.com/themeselection/sneat-bootstrap-html-admin-template-free" data-icon="octicon-star" data-size="large" data-show-count="true" aria-label="Star themeselection/sneat-html-admin-template-free on GitHub">Star</a>
        </li>
      
      <!-- User -->
      <li class="nav-item navbar-dropdown dropdown-user dropdown">
        <a class="nav-link dropdown-toggle hide-arrow p-0" href="javascript:void(0);" data-bs-toggle="dropdown">
          <div class="avatar avatar-online">
            <img src="../assets/img/avatars/Me.png" alt="" class="w-px-40 h-auto rounded-circle">
          </div>
        </a>
        <ul class="dropdown-menu dropdown-menu-end">
          <li>
            <a class="dropdown-item" href="#">
              <div class="d-flex">
                <div class="flex-shrink-0 me-3">
                  <div class="avatar avatar-online">
                    <img src="../assets/img/avatars/Me.png" alt="" class="w-px-40 h-auto rounded-circle">
                  </div>
                </div>
                <div class="flex-grow-1">
                  <h6 class="mb-0">John Doe</h6>
                  <small class="text-body-secondary">Admin</small>
                </div>
              </div>
            </a>
          </li>
          <li>
            <div class="dropdown-divider my-1"></div>
          </li>
          <li>
            
          </li>
          <li>
           
          </li>
          <li>
            <div class="dropdown-divider my-1"></div>
          </li>
          <li>
            <a class="dropdown-item" href="javascript:void(0);" @click="Logout()"> <i class="icon-base bx bx-power-off icon-md me-3"></i><span>ອອກຈາກລະບົບ</span> </a>
          </li>
        </ul>
      </li>
      <!--/ User -->
    
  </ul>
</div>

</nav>

<!-- / Navbar -->
      

      <!-- Content wrapper -->
      <div class="content-wrapper">
        

        <!-- Content -->
  <div class="container-xxl flex-grow-1 container-p-y">
          
     <router-view></router-view>

   </div>
  <!-- / Content -->
        
        

<!-- Footer -->

<!-- / Footer -->

        
        <div class="content-backdrop fade"></div>
      </div>
      <!-- Content wrapper -->
    </div>
    <!-- / Layout page -->
  </div>

  
  
  <!-- Overlay -->
  <div class="layout-overlay layout-menu-toggle"></div>
  
  
</div>
<!-- / Layout wrapper -->

</template>
<script>
import axios from 'axios';
import { useAuthStore } from './Stores/Auth';

export default {
    setup() {
        const authStore = useAuthStore();
        return { authStore };
    },
    methods: {
        Logout() {
            
            axios.get('/api/logout',{
                headers: {
                  Authorization: `Bearer ${this.authStore.getToken}`
                }
            }).then(response => {

              if(response.data.success){
                this.authStore.logout();
                this.$router.push({ name: 'Login' });
              } else {
                console.log('Logout failed:', response.data.message);
              }
          
            }).catch(error => {
                console.error('Logout error:', error);
            });

        }
    }
}

</script>
<style lang="">
    
</style>
