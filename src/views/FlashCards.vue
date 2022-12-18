<template>
  <h1>Welcome to the Quiz</h1>
  <div class="container-fluid">
    <div class="row row-cols-1 row-cols-md-2 g-4">
      <div class="col" v-for="flashcard in flashcards" :key="flashcard.id">
        <div class="col">-->
          <div class="card h-100">
            <img src="../assets/background.png" class="card-img-top" :alt="flashcard.subject">
            <div class="card-body">
              <h5 class="card-title">{{ flashcard.subject }}</h5>
              <p class="card-text">{{ flashcard.question }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'FlashCards',
  data () {
    return {
      flashcards: []
    }
  },
  mounted () {
    const requestOptions = {
      method: 'GET',
      redirect: 'follow'
    }

    fetch('http://localhost:8080/api/v1/flashcards', requestOptions)
      .then(response => response.json())
      .then(result => result.forEach(flashcard => {
        this.flashcards.push(flashcard)
      }))
      .catch(error => console.log('error', error))
  }
}
</script>

<style scoped>

</style>
