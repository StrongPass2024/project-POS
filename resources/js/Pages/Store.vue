<template lang="">
      <div class="row">
        <div class="col-md-14">
            <div class="card">
      <h5 class="card-header fw-semibold" style="color: var(--bs-black);">ລາຍການສິນຄ້າ</h5>
    <div class="card-body">

        <div class="row">
            <div class="col-lg-6 d-flex align-items-center mb-4">
                <div class="me-2">
                  <i class='bx bx-sort-up fs-4'></i>
                  <i class='bx bx-sort-down fs-4'></i>
                </div>
                <select class="form-select w-auto me-2 fw-semibold" style="border-color: var(--bs-gray);">
                    <option value="10">10</option>
                    <option value="20">20</option>
                    <option value="30">30</option>
              </select>

              <select class="form-select w-auto fw-semibold" style="border-color: var(--bs-gray);">
                    <option :value="category.id" v-for="category in Categories" :key="category.id">{{ category.CategoryName }}</option>
              </select>

            </div>
            <div class="col-lg-6 mb-4 d-flex align-items-center justify-content-end">
                <div class="input-group input-group-merge w-auto me-3 fw-semibold">
                  <span class="input-group-text" id="basic-addon-search31" style="border-color: var(--bs-gray);"><i class="icon-base bx bx-search"></i></span>
                  <input type="text" class="form-control" style="border-color: var(--bs-gray);" placeholder="ຄົ້ນຫາ...">
                </div>
                <button type="button" class="btn btn-dark fw-normal" @click="AddProduct()">ເພີ່ມສິນຄ້າ</button>
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
          <tbody class="table-border-bottom-0">
            <tr>
              <td><i class="icon-base fab fa-angular icon-md text-danger me-4"></i> <span>Angular Project</span></td>

              <td>Albert Cook</td>
              <td>Albert Cook</td>
              <td>Albert Cook</td>
              <td>Albert Cook</td>
              <td>Albert Cook</td>
              <td>Albert Cook</td>
              
              <td>
                <div class="dropdown">
                  <button type="button" class="btn p-0 dropdown-toggle hide-arrow" data-bs-toggle="dropdown"><i class="icon-base bx bx-dots-vertical-rounded"></i></button>
                  <div class="dropdown-menu">
                    <a class="dropdown-item" href="javascript:void(0);"><i class="icon-base bx bx-edit-alt me-1"></i> Edit</a>
                    <a class="dropdown-item" href="javascript:void(0);"><i class="icon-base bx bx-trash me-1"></i> Delete</a>
                  </div>
                </div>
              </td>
            </tr>
          </tbody>
        </table>
        </div>
      </div>
    </div>
  </div>
</div>

<div class="modal modal-top fade" id="StoreModal" tabindex="-1" style="display: none;" aria-hidden="true">
                  <div class="modal-dialog modal-lg">
                    <form class="modal-content">
                      <div class="modal-header">
                        <h5 class="modal-title" id="modalTopTitle">Modal title</h5>
                        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                      </div>
                      <div class="modal-body">
                        <div class="row">
                          <div class="col mb-6">
                            <label for="nameSlideTop" class="form-label">Name</label>
                            <input type="text" id="nameSlideTop" class="form-control" placeholder="Enter Name">
                          </div>
                        </div>
                        <div class="row g-6">
                          <div class="col mb-0">
                            <label for="emailSlideTop" class="form-label">Email</label>
                            <input type="email" id="emailSlideTop" class="form-control" placeholder="xxxx@xxx.xx">
                          </div>
                          <div class="col mb-0">
                            <label for="dobSlideTop" class="form-label">DOB</label>
                            <input type="date" id="dobSlideTop" class="form-control">
                          </div>
                        </div>
                      </div>
                      <div class="modal-footer">
                        <button type="button" class="btn btn-dark">ບັນທຶກ</button>
                        <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">ຍົກເລີກ</button>
                      </div>
                    </form>
                  </div>
                </div>
</template>
<script>
import { useAuthStore } from '../Stores/Auth';
import axios from 'axios';

export default {
  setup() {
    const authStore = useAuthStore();
    return { authStore };
  },
    data() {
      return {
          Categories: [],
      };
    },
    methods: {
        AddProduct(){
            $('#StoreModal').modal('show');
        },
        GetCate(){
           axios.get('/api/categories', {
              headers: {
                Authorization: `Bearer ${this.authStore.token}`,
              },
           })
             .then(response => {
               this.Categories = response.data;
             })
             .catch(error => {
               console.error('Error fetching categories:', error);
             });
        }
    },
    created() {
        this.GetCate();
    }

}
</script>
<style lang="">

</style>