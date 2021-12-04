<template>
  <div class="content">
    <div class="title">
      <h1>Nouvautés {{ sexe }} {{ prices }} {{ color }} ({{ completProduct.length }})</h1>
    </div>
    <div class="store">
      <div class="filter">
        <div class="filter-sexe">
          <div class="top">
            <span>Sexe ({{nb_sexe_filter}})</span>
            <i class="fas fa-chevron-up"></i>
          </div>
          <div class="bottom">
            <div class="sexe" v-for="sexe in product_sexe" :key="sexe">
              <input type="checkbox" :value="sexe">
              <label>{{ sexe }}</label>
            </div>
          </div>
        </div>
        <div class="filter-prix"></div>
        <div class="filter-couleur"></div>
        <div class="filter-sport"></div>
      </div>
      <div class="shoes">
        <div class="shoes-elem" v-for="elem in completProduct" :key="elem.prix">
          <div class="img">
            <img class="shoes-img" :src="'/src/images/'+elem.photo" :alt="elem.article"/>
          </div>
          <div class="elem-infos">
            <p class="elem-name">{{ elem.article }}</p>
            <p class="elem-sexe">Chaussure {{ elem.sexe }}</p>
            <p class="elem-couleur">{{ elem.nb_couleur }}</p>
            <p class="elem-prix">{{ elem.prix }}</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import products from "../produits.json"
import Pluralize from 'pluralize';

export default {
  name: 'HelloWorld',
  data() {
    return {
      products: products
    }
  },
  props: {
    msg: String
  },
  computed: {
    completProduct: function() {
      return this.products.filter(function(u) {
        if (u.prix != "") {
          var nb_couleur = u.couleur.split(',').length;
          u.nb_couleur = nb_couleur + ' ' + Pluralize( 'Couleur', u.nb_couleur );
          return u;
        }
      })
    },
    product_sexe: function() {
      return this.products.filter(function(u) {
        if (u.prix != "") {
          return u.sexe
        }
      })
    }
  }
}
</script>
