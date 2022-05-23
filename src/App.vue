<script>
import { RouterView } from 'vue-router'
import { ref } from "vue";
import axios from "axios";
import FooterItem from "./components/FooterItem.vue";

export default {
  data()
  {
    return {
      error: false,
      loading: true,
      juzs: ref([]),
      surahs: ref([])
    }
  },

  components: {
    FooterItem,
    RouterView
  },

  mounted()
  {
    this.getJuz()
    this.getSurah()
  },

  methods: {
    getJuz()
    {
      axios.get('https://api.quran.com/api/v4/juzs')
        .then(response =>
        {
          this.juzs = response.data.juzs
        })
        .catch(error =>
        {
          console.log(error)
          this.error = true
        })
        .finally(() => this.loading = false)
    },
    getSurah()
    {
      axios.get('https://api.quran.com/api/v4/chapters')
        .then(response =>
        {
          this.surahs = response.data.chapters
        })
        .catch(error =>
        {
          console.log(error)
          this.error = true
        })
        .finally(() => this.loading = false)
    },
  }
}
</script>

<template>
    <section v-if="error">
      <div class="container">
        <h1 class="text-center">KODINGAN ERROR!</h1>
      </div>
    </section>

    <section v-else>
      <div v-if="loading" class="container">
        <h1 class="text-center">Loading...</h1>
      </div>

      <div v-else class="container" >
        <nav class="nav navbar-expand-lg navbar-light shadow-sm ">
          <div class="container-fluid">
            <a class="navbar-brand" href="" >
              <img src="/src/assets/al-quran.png" alt="" width="30" height="24" class="d-inline-block align-text-top"  >
              Al-Qur'an API Raudyah
            </a>
          </div>
          <div class="collapse navbar-collapse " id="navbarNavAltMarkup">
            <ul class="navbar-nav nav-pills ms-auto">
              <li class="y nav-item">
                <router-link :to="{ name: 'home' }" class="x nav-link" >Home</router-link>
              </li>
              <li class="y nav-item dropdown">
                <a class="nav-link dropdown-toggle" data-bs-toggle="dropdown" href="#" role="button"
                   aria-expanded="false" >Juz</a>
                <ul class="dropdown-menu">
                  <li v-for="juz in juzs" :key="juz.id">
                    <router-link :to="{ name: 'juzs', params: { id: juz.id } }" class="x dropdown-item">{{ juz.juz_number }}
                    </router-link>
                  </li>
                </ul>
              </li>
              <li class="y nav-item dropdown">
                <a class="nav-link dropdown-toggle" data-bs-toggle="dropdown" href="#" role="button "
                   aria-expanded="false" >Surah</a>
                <ul class="dropdown-menu">
                  <li v-for="surah in surahs" :key="surah.id">
                    <router-link :to="{ name: 'surahs', params: { id: surah.id } }" class="x dropdown-item">{{
                        surah.name_simple
                      }}</router-link>
                  </li>
                </ul>
              </li>
              <li class="y nav-item">
                <router-link :to="{ name: 'search' }" class="x nav-link" >Search</router-link>
              </li>
            </ul>
          </div>
        </nav>
        <RouterView />
      </div>
    </section>
  <FooterItem/>
</template>

<style>
.container {
  margin-bottom: 230%;
}
.nav {
  background: linear-gradient(45deg, #7da4a4, #90c6ba);
  animation: hue-rotate 1s linear infinite alternate;
}

@keyframes hue-rotate {
  to{filter: hue-rotate(90deg);}
}

.nav-item {
  background-image: linear-gradient(transparent 0%, transparent 90%, #dcaa8d 90%, rgb(229, 229, 229) 100%);
  background-repeat: no-repeat;
  background-size: 0% 100%;
  background-position-x: right;
  transition: background-size 300ms;
}

.nav-item:hover{
  background-size: 100% 100%;
  background-position-x: left;
}
</style>
