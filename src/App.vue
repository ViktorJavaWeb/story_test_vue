<template>
  <div class="app">

    <button @click="fetchGet">Заповнити таблицю</button>
    <table class="post">
      <thead>
      <th>nameProduct</th>
      <th>nameBrand</th>
      <th>nameModel</th>
      <th>nameColor</th>
      <th>nameDescription</th>
      <th>foto</th>
      <th>update/delete</th>
      </thead>
      <tbody>
      <tr v-for="post in posts" :key="post.id">
        <td>{{ post.product }}</td>
        <td>{{ post.brand }}</td>
        <td>{{ post.model }}</td>
        <td>{{ post.color }}</td>
        <td>{{ post.descriptionProduct }}</td>
        <td>{{ post.photoProduct }}</td>
        <td><button>updateProduct</button><button>deleteProduct</button></td>
      </tr>
      </tbody>
    </table>


  </div>
</template>


<script>
import axios from 'axios'

export default {
  data() {
    return {
      posts: [],
    }
  },
  methods: {
    async fetchGet() {
      try {
        const response = await axios.get('http://localhost:8080/prod/all');

       this.ar = response.data ;

        console.log(this.ar);

        for (var i = 0; i < this.ar.length; i++) {
          var arS = {};

          arS['product'] = this.ar[i]['product'];
          console.log(arS['nameProduct']);

          arS['brand'] = this.ar[i]['brand'];
          console.log(arS['brand']);

          arS['model'] = this.ar[i]['model'];
          console.log(arS['model']);

          arS['color'] = this.ar[i]['color'];
          console.log(arS['color']);

          arS['description'] = this.ar[i]['description'];
          console.log(arS['description']);

        /*  arS['photoProduct'] = this.ar[i]['photoProduct'];
          console.log(arS['photoProduct']);*/

          this.posts[i] = arS;
        }


      } catch (e) {
        alert('Error')
      }
    }
  }

}
</script>


<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}


table {
  width: 50%; /* Ширина таблицы */
  border: 4px double black; /* Рамка вокруг таблицы */
  border-collapse: collapse; /* Отображать только одинарные линии */
}

th {
  text-align: left; /* Выравнивание по левому краю */
  background: #ccc; /* Цвет фона ячеек */
  padding: 5px; /* Поля вокруг содержимого ячеек */
  border: 1px solid black; /* Граница вокруг ячеек */
}

td {
  padding: 5px; /* Поля вокруг содержимого ячеек */
  border: 1px solid black; /* Граница вокруг ячеек */
}

.btn {
  padding: 2px; /* Поля вокруг содержимого ячеек */
  border: 1px solid black; /* Граница вокруг ячеек */
  background: #ccc; /* Цвет фона ячеек */

}

</style>