<template>
  <div class="container py-5">
    <datavue source="/products" per-page="10">
      <template #title>
        <h2>Products Table</h2>
      </template>
      <template #head>
        <tr>
          <th>Name</th>
          <th>Price</th>
        </tr>
      </template>
      <template #body="{ records }">
        <tr v-for="product in records" :key="product.id">
          <td>{{ product.name }}</td>
          <td>{{ product.price }}</td>
        </tr>
      </template>
    </datavue>
  </div>
</template>
