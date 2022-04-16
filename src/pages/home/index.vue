<script setup lang="ts">
import { ref } from "vue";
import Navbar from "../../components/common/navbar/navbar.vue";
import Banner from "../../components/core/banner/banner.vue";
import Carrousel from "../../components/core/carousel/carousel.vue";
import Card from "../../components/core/card/card.vue";
import Modal from "../../components/common/modal/modal.vue";

const isBannerShow = ref(true);
const isProductModalShow = ref(false);
const currentIndex = ref(0);
const productName = ref("");
const productPrice = ref(0);
const productStock = ref(0);
const productQty = ref(0);

const closeBanner = () => {
  isBannerShow.value = false;
};

const closeModal = () => {
  isProductModalShow.value = false;
  productName.value = "";
  productPrice.value = 0;
  productStock.value = 0;
  productQty.value = 0;
};

const showModal = (item: string, index: number) => {
  isProductModalShow.value = true;
  productName.value = item.name;
  productPrice.value = item.price;
  productStock.value = item.stock;
  currentIndex.value = index;
  console.log(index);
};

const productList = ref([
  {
    id: 1,
    name: "Cappucino Numero uno",
    price: "300",
    desc: "Cappucino dengan rasa unik dan enak serta nikmat sekali",
    stock: 5,
  },
  {
    id: 2,
    name: "Mocahino Uhuy Ahay",
    price: "200",
    desc: "Kopi denga mochachino special yang memiliki rasa unik dan khas",
    stock: 20,
  },
  {
    id: 3,
    name: "Latte Banana",
    price: "200",
    desc: "Kopi enak dengan extract pisang",
    stock: 20,
  },
  {
    id: 4,
    name: "Istant Gulgatos",
    price: "200",
    desc: "Pod bagus asep nya banyak",
    stock: 20,
  },
]);

const addQty = (isDecrease: boolean) => {
  if (isDecrease) {
    if (productQty.value === 0 || productQty.value < 0) {
    } else {
      productQty.value--;
    }
  } else {
    if (productStock.value < productQty.value) {
    } else {
      productQty.value++;
    }
  }
};

const submitData = (index: number) => {
  isProductModalShow.value = false;
  const currentStock = productList.value[index].stock;
  productList.value[index].stock = currentStock - productQty.value;
  if (productStock.value <= 1) {
    productList.value.splice(index, 1);
  }
  productQty.value = 0;
};
</script>
<template>
  <Banner @closeBanner="closeBanner()" v-show="isBannerShow" />
  <Navbar />
  <Carrousel />
  <div class="grid p-24 gap-4 md:grid-cols-4 grid-cols-2">
    <div v-for="(item, index) in productList" :key="index">
      <Card
        @click="showModal(item, index)"
        :title="item.name"
        :desc="item.desc"
        :pic="item.pic"
        :price="item.price"
        :stock="item.stock"
      />
    </div>
    <Modal
      v-if="isProductModalShow"
      :title="productName"
      @submitModal="submitData(currentIndex)"
      @closeModal="closeModal()"
    >
      <div class="flex flex-col mb-6">
        <span class="text-blue-400 font-medium">Mau Beli berapa?</span>
        <button
          @click="addQty()"
          class="bg-blue-400 font-bold text-white p-2 w-1/2 h-auto"
        >
          +</button
        >{{ productQty
        }}<button
          @click="addQty(true)"
          class="bg-blue-400 font-bold p-2 text-white w-1/2 h-auto"
        >
          -
        </button>
      </div>
      <h1 class="text-black-900 font-bold">
        Anda harus membayar Rp.{{ productPrice * productQty }}
      </h1>
    </Modal>
  </div>
</template>
