<template>
  <div>
    <city-header></city-header>
    <city-search :cities="cities"></city-search>
    <city-list :hot="hotCities" :cities="cities" :letter="letter"></city-list>
    <city-alphabet :cities="cities" @change="handleLetterChange"></city-alphabet>
  </div>
</template>

<script>
import CityHeader from './components/Header'
import CitySearch from './components/Search'
import CityList from './components/List'
import CityAlphabet from './components/Alphabet'
import axios from 'axios'

export default {
  name: 'City',
  components: {
    CityHeader,
    CitySearch,
    CityList,
    CityAlphabet
  },
  data () {
    return {
      cities: {},
      hotCities: [],
      letter: ''
    }
  },
  methods: {
    getCityInfo () {
      axios.get('https://www.easy-mock.com/mock/5ca56f0706e65a2e94712962/api/city')
        .then(this.getCityInfoSucc)
    },
    getCityInfoSucc (res) {
      res = res.data
      const data = res.data
      this.cities = data.cities
      this.hotCities = data.hotCities
    },
    handleLetterChange (letter) {
      this.letter = letter
    }
  },
  mounted () {
    // test
    this.getCityInfo()
  }
}
</script>

<style lang="stylus" scoped>

</style>
