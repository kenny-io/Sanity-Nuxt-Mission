<template>
  <div class="container">
    <div class="card">
      <div>
        <img :src="product.imageUrl" alt="Product image" style="width:100%" />
      </div>
      <div class="details">
        <h1>{{ product.title }}</h1>
        <div class="price">
          <h3>${{ product.price }}</h3>
        </div>
        <div class="description">
          <p style="display: block;">
            Lorem, ipsum dolor sit amet consectetur adipisicing elit. Ratione,
            dicta atque excepturi, repellat neque natus reprehenderit molestiae
            placeat harum perferendis, recusandae ipsa debitis a itaque
            doloremque eius numquam voluptatum ex.
          </p>
        </div>
        <div class="quantity">
          <h3>QUANTITY</h3>
          <input type="number" name="items" id="counter" min="1" value="1" />
        </div>
        <div class="buttons">
          <button>
            ADD TO CART
          </button>
          <button>BUY NOW</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { groq } from "@nuxtjs/sanity";
export default {
  async asyncData({ params, $sanity }) {
    const query = groq`
      *[_type == "product" && slug.current == "${params.slug}" ][0]{
        title,
        slug,
        _id,
        "price": defaultProductVariant.price,
        "imageUrl": defaultProductVariant.images[0].asset->url,
        "blurb": blurb.en
      }`;
    const product = await $sanity.fetch(query);
    return { product };
  }
};
</script>

<style>
* {
  margin: 0px;
  padding: 0px;
}

html,
body {
  margin: 0px;
  padding: 0px;
  height: 100%;
  width: 100%;
  overflow-x: hidden;
}

body {
  font-family: "Montserrat", sans-serif;
  background-color: rgb(216, 216, 216);
}

.container {
  height: 100%;
  padding: 20px;
}

.card {
  background-color: white;
  display: flex;
  align-items: center;
  justify-content: space-between;
  flex-direction: column;
  position: relative;
  width: 1140px;
}

.details h1 {
  display: none;
}

.price {
  display: flex;
  justify-content: flex-start;
  margin-top: 0.5rem;
  color: rgb(10, 159, 170);
}
/* 
#more-details {
  display: flex;
  justify-content: space-between;
  color: gray;
}

#more-details h5 {
  padding: 8px;
}
#more-details h5:nth-child(1) {
  color: black;
  border-bottom: 2px solid black;
  padding-bottom: 6px;
} */

.details {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  height: 400px;
  margin-top: 30px;
  width: 90%;
}

.choose {
  cursor: pointer;
}

.quantity {
  width: 60%;
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-top: 20px;
}

.quantity input {
  text-align: center;
  width: 40px;
}

.description {
  font-size: 16px;
  margin-top: 0.5rem;
}

.buttons {
  height: 40px;
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 1rem;
}

button {
  margin: 10px;
  width: 180px;
  padding: 5px;
  font: inherit;
  border: 2px solid #5fdffc;
  border-radius: 25px;
  background-color: white;
  outline: none;
  cursor: pointer;
}

button:nth-child(1) i {
  margin-right: 1rem;
}

button:hover {
  color: white;
  background-color: #5fdffc;
}

@media (min-width: 1025px) {
  body {
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .container {
    width: 100vw;
    height: 80%;
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 20px;
  }

  .card {
    flex-direction: row;
    height: 85%;
    width: 80%;
    border-radius: 15px;
  }

  .details {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    margin-top: 0px;
    height: 80%;
    width: 50%;
    font-size: 20px;
    padding-right: 70px;
  }

  .details h1 {
    display: block;
  }

  .buttons {
    flex-direction: row;
    font-size: 15px;
  }
  .buttons button {
    padding: 8px;
  }
}

@media (min-width: 670px) {
  .container {
    display: flex;
    align-items: center;
    justify-content: center;
  }
  .buttons {
    flex-direction: row;
    font-size: 15px;
  }

  .card {
    width: 75%;
    height: 100%;
  }
}
</style>
