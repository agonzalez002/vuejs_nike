<template>
  <div class="content">
    <div class="title">
      <h1>
        Nouvautés
        <span v-for="count_sexe in filtreSexe" :key="count_sexe"> - {{ count_sexe }} </span>
        <span v-for="count_prices in filtrePrix" :key="count_prices"> - {{ count_prices }} </span>
        <span v-for="count_couleur in filtreCouleur" :key="count_couleur"> - {{ count_couleur }} </span>
        <span v-for="count_sport in filtreSport" :key="count_sport"> - {{ count_sport }} </span>
        ({{ completProduct.length }})
      </h1>
      <i class="fas fa-bars" v-on:click="close_menu()"></i>
    </div>
    <div class="mobile-menu" v-bind:class="{show: mobileMenu}">
      <i class="fas fa-times-circle" v-on:click="close_menu()"></i>
      <div class="filter">
        <div class="filter-elem">
          <div class="top" v-on:click="toogle_sexe()">
            <span>Sexe ({{ filtreSexe.length }})</span>
          </div>
          <div class="bottom">
            <label class="label sexe" v-for="sexe_filter in product_sexe" :key="sexe_filter">
              {{ sexe_filter }}
              <input type="checkbox" :value="sexe_filter" v-model="filtreSexe">
              <span class="custom_input"></span>
            </label>
          </div>
        </div>
        <div class="filter-elem">
          <div class="top" v-on:click="toogle_prix()">
            <span>Prix ({{filtrePrix.length}})</span>
          </div>
          <div class="bottom">
            <label class="label prix" v-for="prix_filter in product_prix" :key="prix_filter">
              {{ prix_filter }}
              <input type="checkbox" :value="prix_filter" v-model="filtrePrix">
              <span class="custom_input"></span>
            </label>
          </div>
        </div>
        <div class="filter-elem">
          <div class="top" v-on:click="toogle_couleur()">
            <span>Couleur ({{filtreCouleur.length}})</span>
          </div>
          <div class="bottom couleur">
            <div class="each-color" v-for="couleur_filter in product_couleur" :key="couleur_filter">
              <label class="label couleur">
                <input type="checkbox" :value="couleur_filter" v-model="filtreCouleur">
                <span :class="'custom_input couleur ' + couleur_filter" :style="{ 'background-color': color_translate[couleur_filter] }"></span>
                {{ couleur_filter }}
              </label>
            </div>
          </div>
        </div>
        <div class="filter-elem">
          <div class="top" v-on:click="toogle_sport()">
            <span>Sport ({{filtreSport.length}})</span>
          </div>
          <div class="bottom">
            <label class="label sport" v-for="sport_filter in product_sport" :key="sport_filter">
              {{ sport_filter }}
              <input type="checkbox" :value="sport_filter" v-model="filtreSport">
              <span class="custom_input"></span>
            </label>
          </div>
        </div>
        <div class="btns">
          <a href="javascript:void(0)" class="btn remove_filter" v-on:click="remove_filter()">Effacer ({{ filtreSexe.length + filtrePrix.length + filtreCouleur.length + filtreSport.length}})</a>
          <a href="javascript:void(0)" class="btn apply_filter" v-on:click="close_menu()">Appliquer</a>
        </div>
      </div>
    </div>
    <div class="store" v-bind:class="{show: mobileMenu}">
      <div class="filter">
        <div class="filter-elem" v-bind:class="{show: filterSexe}">
          <div class="top" v-on:click="toogle_sexe()">
            <span>Sexe ({{ filtreSexe.length }})</span>
            <i class="fas fa-chevron-up"></i>
            <i class="fas fa-chevron-down"></i>
          </div>
          <div class="bottom">
            <label class="label sexe" v-for="sexe_filter in product_sexe" :key="sexe_filter">
              {{ sexe_filter }}
              <input type="checkbox" :value="sexe_filter" v-model="filtreSexe">
              <span class="custom_input"></span>
            </label>
          </div>
        </div>
        <div class="filter-elem" v-bind:class="{show: filterPrix}">
          <div class="top" v-on:click="toogle_prix()">
            <span>Prix ({{filtrePrix.length}})</span>
            <i class="fas fa-chevron-up"></i>
            <i class="fas fa-chevron-down"></i>
          </div>
          <div class="bottom">
            <label class="label prix" v-for="prix_filter in product_prix" :key="prix_filter">
              {{ prix_filter }}
              <input type="checkbox" :value="prix_filter" v-model="filtrePrix">
              <span class="custom_input"></span>
            </label>
          </div>
        </div>
        <div class="filter-elem" v-bind:class="{show: filterCouleur}">
          <div class="top" v-on:click="toogle_couleur()">
            <span>Couleur ({{filtreCouleur.length}})</span>
            <i class="fas fa-chevron-up"></i>
            <i class="fas fa-chevron-down"></i>
          </div>
          <div class="bottom couleur">
            <div class="each-color" v-for="couleur_filter in product_couleur" :key="couleur_filter">
              <label class="label couleur">
                <input type="checkbox" :value="couleur_filter" v-model="filtreCouleur">
                <span :class="'custom_input couleur ' + couleur_filter" :style="{ 'background-color': color_translate[couleur_filter] }"></span>
                {{ couleur_filter }}
              </label>
            </div>
          </div>
        </div>
        <div class="filter-elem" v-bind:class="{show: filterSport}">
          <div class="top" v-on:click="toogle_sport()">
            <span>Sport ({{filtreSport.length}})</span>
            <i class="fas fa-chevron-up"></i>
            <i class="fas fa-chevron-down"></i>
          </div>
          <div class="bottom">
            <label class="label sport" v-for="sport_filter in product_sport" :key="sport_filter">
              {{ sport_filter }}
              <input type="checkbox" :value="sport_filter" v-model="filtreSport">
              <span class="custom_input"></span>
            </label>
          </div>
        </div>
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
      filterSexe: true,
      filterPrix: true,
      filterCouleur: true,
      filterSport: true,
      mobileMenu: false,
      products: products,
      product_prix: ["Moins €50", "€50 - €100", "€100 - €150", "Plus de €150"],
      product_trans: {
        "Moins €50": {
          "min": 0,
          "max": 50
        },
        "€50 - €100": {
          "min": 50,
          "max": 100
        },
        "€100 - €150": {
          "min": 100,
          "max": 150
        },
        "Plus de €150": {
          "min": 150,
          "max": 9999
        }
      },
      nb_sexe_filter: 0,
      nb_couleur_filter: 0,
      nb_prix_filter: 0,
      nb_sport_filter: 0,
      sexe: '',
      prices: '',
      color: '',
      color_translate: {
        "Noir": "black",
        "Rouge": "red",
        "Blanc": "white",
        "Jaune": "yellow",
        "Bleu": "blue",
        "Rose": "pink",
        "Vert": "green",
        "Gris": "gray",
      },
      filtreSexe: [],
      filtrePrix: [],
      filtreCouleur: [],
      filtreSport: [],
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
          return u
        }
      }).filter((item) => {
        return (this.filtreSexe.length === 0 || this.filtreSexe.includes(item.sexe)) &&
        (this.filtreSport.length === 0 || this.filtreSport.includes(item.sport))
      }).filter((item) => {
        if (this.filtrePrix.length === 0) {
          return item
        } else {
          for (var i in this.filtrePrix) {
            var min_price = this.product_trans[this.filtrePrix[i]]['min']
            var max_price = this.product_trans[this.filtrePrix[i]]['max']
            if (min_price <= parseInt(item.prix) && parseInt(item.prix) <= max_price) {
              return item
            }
          }
        }
      }).filter((item) => {
        if (this.filtreCouleur.length === 0) {
          return item
        } else {
          for (var i in this.filtreCouleur) {
            var item_color = [];
            var color = this.filtreCouleur[i].toLowerCase();
            Array.prototype.push.apply(item_color, item.couleur.split(','));
            item_color = item_color.map(color => {
              return color.trim().toLowerCase();
            })

            if (item_color.indexOf(color) > -1) {
              return item
            }
          }
        }
      })
    },
    product_sexe: function() {
      var sexe = [];
      for (var i in this.products) {
        if (this.products[i]['sexe'] != "") {
          sexe.push(this.products[i]['sexe']);
        }
      }
      return new Set(sexe);
    },
    product_couleur: function() {
      var couleur = [];
      for (var i in this.products) {
        if (this.products[i]['couleur'] != "") {
          Array.prototype.push.apply(couleur, this.products[i]['couleur'].split(','));
        }
      }
      couleur = couleur.map(color => {
        var col = color.trim().toLowerCase();
        return col.charAt(0).toUpperCase() + col.slice(1);
      })
      return new Set(couleur);
    },
    product_sport: function() {
      var sport = [];
      for (var i in this.products) {
        if (this.products[i]['sport'] != "") {
          sport.push(this.products[i]['sport']);
        }
      }
      return new Set(sport);
    },
  },
  methods: {
    toogle_sexe() {
      this.filterSexe = !this.filterSexe;
    },
    toogle_prix() {
      this.filterPrix = !this.filterPrix;
    },
    toogle_couleur() {
      this.filterCouleur = !this.filterCouleur;
    },
    toogle_sport() {
      this.filterSport = !this.filterSport;
    },
    close_menu() {
      this.mobileMenu = !this.mobileMenu;
    },
    remove_filter() {
      this.filtreSexe = [];
      this.filtrePrix = [];
      this.filtreCouleur = [];
      this.filtreSport = [];
    }
  }
}
</script>
