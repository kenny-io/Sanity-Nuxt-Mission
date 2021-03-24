<template>
  <div class="wrapper">
    <h2>All Snack Products</h2>
    <p>
      Navigate through our list of products and order your favorite snack!
    </p>
    <div v-for="product in products" :key="product._id" class="products">
      <div class="title">
        <h3>{{ product.title }}</h3>
        <p>{{ product.blurb }}</p>
      </div>
      <div class="content">
        <div class="BOX">
          <div class="pic">
            <img :src="product.imageUrl" alt="" />
          </div>
        </div>
      </div>

      <div class="more">
        <nuxt-link :to="product.slug.current">
          <p>Learn more ></p>
        </nuxt-link>
      </div>
    </div>
  </div>
</template>

<script>
import { groq } from "@nuxtjs/sanity";
export default {
  async asyncData({ $sanity }) {
    const query = groq`
      *[_type == "product"]{
        title,
        slug,
        _id,
        "price": defaultProductVariant.price,
        "imageUrl": defaultProductVariant.images[0].asset->url,
        "blurb": blurb.en
      }`;
    const products = await $sanity.fetch(query);
    return { products };
  }
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  list-style-type: none;
  font-family: "Comic Sans MS";
}

body {
  background-color: #eee;
}

.wrapper {
  width: 100vw;
  height: 100vh;
  margin: 0 auto;
  text-align: center;
}

.wrapper h2 {
  margin: 20px 0 10px 0;
}

.products {
  width: 300px;
  height: 500px;
  position: relative;
  top: 50px;
  left: 0px;
  border-radius: 10px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.5);
  margin: 20px 0 0 60px;
  background-color: #fff;
  display: inline-block;
  transform-origin: 100% 0;
  margin: 1rem;
}

/* ------------title----------- */
.title {
  width: 100%;
  height: 90px;
  line-height: 25px;
  padding: 25px 25px;
  box-sizing: border-box;
  color: #346;
  margin: 0;
  z-index: 20;
}

/* -----------content div---------- */
.content {
  width: 260px;
  height: 330px;
  margin-left: 20px;
  position: relative;
  left: 0;
  top: 0;
  overflow: hidden;
}

/* -------------------- BOX-------------------------- */
.BOX {
  width: 260px;
  height: 260px;
  position: absolute;
  left: 0px;
  top: 30px;
  transition: 0.5s;
  overflow: hidden;
}

.pic {
  width: 1300px;
  position: relative;
  transition: 0.8s cubic-bezier(0.5, -1, 0.75, 2);
}

.pic img {
  float: left;
  width: 20%;
  height: 20%;
}

/* ------------------Add-to-more button---------------------- */
.more {
  text-align: center;
  padding: 5px 10px;
  width: 230px;
  border-radius: 5px;
  margin: 15px 0 0 23px;
  background-color: #000;
  cursor: pointer;
}
.more p {
  color: #fff;
}

/* ------animation-Add-to-more button--------- */
.more:hover {
  background-color: #346;
  color: #fff;
  transition: 1s;

  animation: wobble 1s ease-in-out 1;
}
a {
  text-decoration: none;
}

@keyframes wobble {
  16.65% {
    transform: translateY(8px);
  }
  33.3% {
    transform: translateY(-6px);
  }
  49.95% {
    transform: translateY(4px);
  }
  66.6% {
    transform: translateY(-2px);
  }
  83.25% {
    transform: translateY(1px);
  }
  100% {
    transform: translateY(0);
  }
}
</style>
