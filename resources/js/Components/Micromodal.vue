<script setup>
import axios from 'axios';
import { reactive, ref } from 'vue';

const search = ref("");
const customers = reactive({});
const isShow = ref(false);

const seachCustomers = async ()=> {
    try {
        await axios.get(`/api/searchCustomers/?search=${search.value}`)
        .then(res=>{
            customers.value = res.data;
        })

        toggleStatus();
    } catch (error) {
        console.log(e.message);
    }
}
const toggleStatus = ()=> {
    isShow.value = !isShow.value
}

</script>

<template>
  <div v-show="isShow" class="modal" id="modal-1" aria-hidden="true">
    <div class="modal__overlay" tabindex="-1" data-micromodal-close>
      <div class="modal__container" role="dialog" aria-modal="true" aria-labelledby="modal-1-title">
        <header class="modal__header">
          <h2 class="modal__title" id="modal-1-title">
            Micromodal
          </h2>
          <button type="button" @click="toggleStatus" class="modal__close" aria-label="Close modal" data-micromodal-close></button>
        </header>
        <main class="modal__content" id="modal-1-content">
          <p>
            Try hitting the <code>tab</code> key and notice how the focus stays within the modal itself. Also, <code>esc</code> to close modal.
          </p>
        </main>
        <footer class="modal__footer">
          <button type="button" @click="toggleStatus" class="modal__btn modal__btn-primary">Continue</button>
          <button type="button" @click="toggleStatus" class="modal__btn" data-micromodal-close aria-label="Close this dialog window">Close</button>
        </footer>
      </div>
    </div>
  </div>
  <input name="customer" v-model="search">
  <button @click="seachCustomers" type="button" data-micromodal-trigger="modal-1">検索する</button>
</template>
