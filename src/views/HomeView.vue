<script setup>
import {ref, onMounted} from 'vue';
import axios from 'axios';


const userValue = ref([])
const objVal = import.meta.env.VITE_APP_BASE_URL;

const currentPage = ref(1);
const itemsPerPage = 50; 
const totalItems = ref(0);
const totalPages = ref(0);

const getData = () =>{
  axios.get(`${objVal}?offset=${(currentPage.value - 1) * itemsPerPage}&limit=${itemsPerPage}`)
        .then((res) =>{
          userValue.value = res.data.users;
          totalItems.value = res.data.total_users;
          totalPages.value = Math.ceil(totalItems.value / itemsPerPage);
            console.log("users>>", userValue.value);
            console.log('total>>', res.data);
            console.log("pageTotal>>", totalPages.value)
        })
}

const prevPage = () => {
  if (currentPage.value > 1) {
    currentPage.value--;
    getData();
  }
  console.log("prev")
};

const nextPage = () => {
  if(currentPage.value < totalPages.value) {
    currentPage.value++;
    getData();
  }
  console.log("next")
};


onMounted(() =>{
  getData();
  console.log("window>>",window)
})
</script>

<template>
  <main>
   <!-- component -->
<div class="flex flex-col">
  <div class="overflow-x-auto sm:mx-0.5 lg:mx-0.5">
    <div class="py-2 inline-block min-w-full sm:px-6 lg:px-8">
      <div class="overflow-hidden">
        <table class="min-w-full">
          <thead class="bg-white border-b">
            <tr>
              <th scope="col" class="text-sm font-medium text-gray-900 px-6 py-4 text-left">
                #
              </th>
              <th scope="col" class="text-sm font-medium text-gray-900 px-6 py-4 text-left">
                Email
              </th>
              <th scope="col" class="text-sm font-medium text-gray-900 px-6 py-4 text-left">
                First Name
              </th>
              <th scope="col" class="text-sm font-medium text-gray-900 px-6 py-4 text-left">
                Last name
              </th>
              <th scope="col" class="text-sm font-medium text-gray-900 px-6 py-4 text-left">
                Gender
              </th>
              <th scope="col" class="text-sm font-medium text-gray-900 px-6 py-4 text-left">
                Country
              </th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="elem in userValue" :key="elem.id" class="bg-gray-100 border-b">
              <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-gray-900">{{elem.id}}</td>
              <td class="text-sm text-gray-900 font-light px-6 py-4 whitespace-nowrap">
                {{elem.email}}
              </td>
              <td class="text-sm text-gray-900 font-light px-6 py-4 whitespace-nowrap">
                {{elem.first_name}}
              </td>
              <td class="text-sm text-gray-900 font-light px-6 py-4 whitespace-nowrap">
                {{elem.last_name}}
              </td>
              <td class="text-sm text-gray-900 font-light px-6 py-4 whitespace-nowrap">
                {{elem.gender}}
              </td>
              <td class="text-sm text-gray-900 font-light px-6 py-4 whitespace-nowrap">
                {{elem.country}}
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>

    <div class="flex justify-center gap-12 py-4">
      <button @click="nextPage" :disabled="currentPage === totalPages" class="bg-indigo-500 px-12 py-1 rounded text-white font-bold hover:text-slate-700 transition ease-in-out duration-500 hover:bg-indigo-200">Next</button>
      <button @click="prevPage" :disabled="currentPage === 1" class="bg-indigo-500 px-8 py-1 rounded text-white transition ease-in-out duration-500 font-bold hover:text-slate-700 hover:bg-indigo-200">Previous</button>
    </div>
  </div>
</div>

  </main>
</template>
