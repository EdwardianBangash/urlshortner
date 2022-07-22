<template>
  <section>
    <div class="container">
      <form @submit.prevent="onSubmit">
        <h1>URL SHORTNER</h1>
        <div class="form-group">
          <label for="url">Url</label>
          <input
            type="text"
            v-model="url"
            placeholder="https://www.example.com"
          />
        </div>
        <input type="submit" value="Submit" />
      </form>
    </div>
    <div class="container" v-if="result.length > 0">
      <div class="result">
        <ul>
          <li v-for="r in result" :key="r.id">
            <a :href="r.short_url"
              >{{ r.short_url }}</a
            >
          </li>
        </ul>
      </div>
    </div>
  </section>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      url: null,
      result: [],
    };
  },
  methods: {
    onSubmit() {
      axios
        .post("/shortner", {
          url: this.url
        })
        .then((response) => {
          this.result = []
            this.result.unshift(response.data.result);
        })
        .catch((error) => {});
    },
  },
};
</script>
<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
section {
  height: 100vh;
}

.container {
  padding-top: 100px;
  width: 100%;
}

form {
  width: 400px;
  margin: 0px auto;
  border-radius: 2px;
  background-color: rgba(236, 223, 223, 0.875);
  padding: 20px;
}

h1 {
  padding: 20px;
  text-align: center;
}
label {
  display: block;
  font-size: 16px;
  font-weight: 700;
  text-transform: uppercase;
  margin-bottom: 5px;
  letter-spacing: 4px;
}

input[type="text"] {
  width: 100%;
  padding: 5px;
  font-size: 18px;
}

input[type="submit"] {
  margin-top: 20px;
  padding: 5px 10px;
  border: none;
  background: rgb(14, 92, 118);
  color: #fff;
  font-size: 15px;
}
div.result {
  background: rgb(207, 203, 203);
  width: 500px;
  margin: 0 auto;
  padding: 20px;
  border-radius: 5px;
}
ul {
  list-style: none;
}
a {
  text-decoration: none;
  color: #000;
}

a:hover {
  text-decoration: underline;
}

li {
  margin-top: 10px;
}
</style>
