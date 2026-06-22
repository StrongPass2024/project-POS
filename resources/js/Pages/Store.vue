<template lang="">
      <div class="row">
        <div class="col-md-14">
    <div class="card">
        <h5 class="card-header fw-semibold" style="color: var(--bs-black);">ລາຍການສິນຄ້າ</h5>
    <div class="card-body">

        <div class="row">
            <div class="col-lg-6 d-flex align-items-center mb-4">
                <div class="me-2" @click="Sort = (Sort === 'asc') ? 'desc' : 'asc'; GetProduct(); " style="cursor: pointer;">
                  <i class='bx bx-sort-up fs-4' v-if="Sort === 'asc'"></i>
                  <i class='bx bx-sort-down fs-4' v-else></i>
                </div>
                <select class="form-select w-auto me-2 fw-semibold" v-model="PerPage" @change="GetProduct()" style="border-color: var(--bs-gray);">
                    <option value="10">10</option>
                    <option value="20">20</option>
                    <option value="30">30</option>
              </select>

              <select class="form-select w-auto fw-semibold" v-model="CategorySelect" @change="GetProduct()" style="border-color: var(--bs-gray);">
                    <option value="all">ໝວດໝູ່ທັງໝົດ</option>
                    <option :value="category.id" v-for="category in Categories" :key="category.id">{{ category.CategoryName }}</option>
              </select>

            </div>
            <div class="col-lg-6 mb-4 d-flex align-items-center justify-content-end">
                <div class="input-group input-group-merge w-auto me-3 fw-semibold">
                  <span class="input-group-text" id="basic-addon-search31" style="border-color: var(--bs-gray);"><i class="icon-base bx bx-search"></i></span>
                  <input type="text" v-model="Search" class="form-control" style="border-color: var(--bs-gray);" placeholder="ຄົ້ນຫາ...." @keyup.enter="GetProduct()">
                </div>
                <button type="button" class="btn btn-dark" @click="AddProduct()">ເພີ່ມສິນຄ້າ</button>
            </div>

          </div> 
          

          <!-- {{ Categories}} -->

      <div class="table-responsive text-nowrap">
        <table class="table table-bordered">
          <thead class="table-dark">
            <tr>
              <th class="fw-semibold fs-6">#</th>
              <th class="fw-semibold fs-6">ຮູບພາບ</th>
              <th class="fw-semibold fs-6">ຊື່ສິນຄ້າ</th>
              <th class="fw-semibold fs-6">ໝວດໝູ່</th>
              <th class="fw-semibold fs-6">ຈຳນວນ</th>
              <th class="fw-semibold fs-6">ລາຄາຊຶ້</th>
              <th class="fw-semibold fs-6">ລາຄາຂາບ</th>
              <th class="fw-semibold fs-6">ແກ້ໄຂ</th>
            </tr>
          </thead>
          
          <tbody v-if="loading">
            <tr>
              <td colspan="8">
                  <div class="d-flex align-items-center justify-content-center"> 
                       <div class="spinner-border text-secondary me-3" role="status">
                        <span class="visually-hidden">ກຳລັງໂຫຼດ...</span>
                     </div> ກຳລັງໂຫຼດ...
                  </div>
              </td>
            </tr>
          </tbody>

          <tbody class="table-border-bottom-0" v-if="!loading">
            <tr v-for="product in ProductsList.data" :key="product.id">
              <td>{{ product.id }}</td>
              <td></td>
              <td>{{ product.ProductName }}</td>
              <td>{{ product.CategoryID }}</td>
              <td>{{ product.Qty }}</td>
              <td>{{ product.PriceBuy }}</td>
              <td>{{ product.PriceSell }}</td>
              <td>
                <div class="dropdown">
                  <button type="button" class="btn p-0 dropdown-toggle hide-arrow" data-bs-toggle="dropdown"><i class="icon-base bx bx-dots-vertical-rounded"></i></button>
                  <div class="dropdown-menu">
                    <a class="dropdown-item fw-semibold" href="javascript:void(0);"><i class="icon-base bx bx-edit-alt me-1"></i>ແກ້ໄຂ</a>
                    <a class="dropdown-item fw-semibold" href="javascript:void(0);"><i class="icon-base bx bx-trash me-1"></i>ລົບ</a>
                  </div>
                </div>
              </td>
            </tr>
          </tbody>
        </table>
         <Pagination :pagination="ProductsList" :offset="4" @paginate="GetProducts($event)" />
        </div>
      </div>
    </div>
  </div>
</div>

<!-- Modal -->
      <div class="modal modal-top fade" id="StoreModal" tabindex="-1" style="display: none;" aria-hidden="true">
              <div class="modal-dialog modal-lg">
                    <form class="modal-content">
                      <div class="modal-header">
                        <h5 class="modal-title fw-semibold" id="modalTopTitle">
                           <span>ເພີ່ມສິນຄ້າ</span>
                           <span>ແກ້ໄຂສິນຄ້າ</span>
                        </h5>
                        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                      </div>
                      <div class="modal-body">
                          <div class="row">
                            <div class="col-lg-4 fw-semibold">ຮູບພາບ</div>
                            <div class="col-lg-8">
                                
                             <div class="row">
                              <div class="col-lg-8 mb-3">
                                <label class="form-label fw-semibold">ຊື່ສິນຄ້າ:</label>
                                <input type="text" v-model="FormProduct.ProductName" class="form-control" placeholder=".......">
                             </div>
                              <div class="col-lg-4 mb-3">
                                  <label class="form-label fw-semibold">ໝວດໝູ່ສິນຄ້າ:</label>
                                  <select class="form-select fw-semibold" v-model="FormProduct.CategoryID" style="border-color: var(--bs-gray);">
                                    <option value="">-- ເລືອກໝວດໝູ່ --</option>
                                      <option :value="category.id" v-for="category in Categories" :key="category.id">{{ category.CategoryName }}</option>
                                  </select>
                              </div>
                            </div>
                       
                       <div class="row">
                            <div class="col-lg-4 mb-3">
                                <label class="form-label fw-semibold">ຈຳນວນ:</label>
                                <input type="number" v-model="FormProduct.Qty" class="form-control" placeholder="......."> 
                            </div>
                       </div>
                       <div class="row">
                            <div class="col-lg-6 mb-3">
                                <label class="form-ladel fw-semibold">ລາຄາຊື້:</label>
                                <input type="number" v-model="FormProduct.PriceBuy" class="form-control" placeholder="......."> 
                            </div>
                            <div class="col-lg-6 mb-3">
                                <label class="form-ladel fw-semibold">ລາຄາຂາຍ:</label>
                                <input type="number" v-model="FormProduct.PriceSell" class="form-control" placeholder="......."> 
                            </div>

                       </div>


                      </div>
                        </div>
                      </div>
                        <div class="modal-footer"> 
                          <button type="button" class="btn btn-dark" :disabled="isFormvalidate" @click="SaveProduct()">ບັນທຶກ</button>
                          <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">ຍົກເລີກ</button>
                        </div>
                    </form>
                </div>
        </div>
</template>
<script>
import { useAuthStore } from "../Stores/Auth";
import axios from "axios";

export default {
  setup() {
    const authStore = useAuthStore();
    return { authStore };
  },
  data() {
    return {
      loading: false,
      Categories: [],
      ProductsList: [],
      formType: true,
      EditID: "",
      FormProduct: {
        ProductName: "",
        CategoryID: "",
        // ImagePath: "",
        Qty: 0,
        PriceBuy: 0,
        PriceSell: 0,
    },
        Sort: 'asc',
        PerPage: 10,
        CategorySelect: 'all',
        Search: '',
    };
  },

   computed: {
        isFormvalidate() {
            if(this.FormProduct.ProductName == "" || this.FormProduct.CategoryID == "" || this.FormProduct.Qty <= 0 || this.FormProduct.PriceBuy <= 0 || this.FormProduct.PriceSell <= 0){
                return true;
            } else {
                return false;
            }
        }  
    },

  methods: {
    AddProduct() {
      this.FormProduct = {
        ProductName: "",
        CategoryID: "",
        // ImagePath: "",
        Qty: 0,
        PriceBuy: 0,
        PriceSell: 0,
      };
      this.formType = true;
      $("#StoreModal").modal("show");
    },

    EditProduct(id) {},
    SaveProduct() {
      if (this.formType) {
        axios
          .post("/api/products/add", this.FormProduct, {
            headers: {
              Authorization: `Bearer ${this.authStore.token}`,
            },
          })
          .then((response) => {
            if (response.data.success) {
              console.log("Product added successfully", response.data);
              $("#StoreModal").modal("hide");
              this.GetProduct();
            } else {
              console.error("Failed to add product", response.data.message);
            }
          })
          .catch((error) => {
            console.error("Error adding product", error);
          });
      } else {
        
      }
    },
    GetProduct(page=1) {
      axios.get(`/api/products?page=${page}&perPage=${this.PerPage}&sort=${this.Sort}&search=${this.Search}&category=${this.CategorySelect}`, {
          headers: {
            Authorization: `Bearer ${this.authStore.token}`,
          },
        })
        .then((response) => {
          this.ProductsList = response.data;
        })
        .catch((error) => {
          console.error("Error fetching products", error);
        });
    },
    GetCate() {
      this.loading = true;
      axios
        .get(`/api/categories`, {
          headers: {
            Authorization: `Bearer ${this.authStore.token}`,
          },
        })
        .then((response) => {
          this.Categories = response.data;
          this.loading = false;
        })
        .catch((error) => {
          console.error("Error fetching categories:", error);
          this.loading = false;
        });
    },
  },
  created() {
    this.GetCate();
    this.GetProduct();
  },
    watch: {
        Search(newVal) {
            if (newVal === '') {
                this.GetProducts();
            }
        }
    }
};
</script>
<style lang="">
</style>