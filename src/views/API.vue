export default {
  methods: {
    async fetchData(ids) {
      const responses = await Promise.all(ids.map(id => window.fetch(`${api}/${id}`)))
      const data = await Promise.all(responses.map(r => r.json()))
      return data.map(d => ({
        id: d.id,
        name: d.name,
        sprite: d.sprites.other['official-artwork'].front_default,
        types: d.types.map(type => type.type.name)
      }))
    },
  },
  watch: {
    async $route(to, from) {
      this.pokemon = (await this.fetchData([this.$route.params.id]))[0]
    },
  },
  data() {
    return {
      pokemon: null,
    }
  },
}