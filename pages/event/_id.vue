<template>
    <div>
        <h1> Event #{{event.title}}</h1>
    </div>
</template>

<script>
export default {
  head() {
    return {
      title: this.event.title,
      meta: [
        {
          hid:'description',
          name: 'description',
          content:
            'What you need to know about Event' + this.id.title
        }
      ] 
    }
},
async asyncData ({$axios, error, params}) {
  try {
    const {data} = await $axios.get('http://localhost:3000/events' + params.id)
      return {
        event: data
      }
  } catch (e) {
    error({
      statusCode: 503,
      message: 'Unable to get events #' + params.id
    })
  }
},

}
</script>