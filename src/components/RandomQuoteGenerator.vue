<template>
    <div class="quote-generator">
        <h1 class="app-title">Random Quote Generator</h1>
        <blockquote class="quote-container">
            <p>{{currentQuote.text}}</p>
            <cite>-- {{currentQuote.author}}</cite>

        </blockquote>
        <button @click="getRandomQuote" class="quote-button">Get Random Quotes</button>
    </div>
</template>

<script setup>
import {ref, onMounted} from 'vue'



const currentQuote = ref({text: '' , author:''})

const getRandomQuote = () => {
    fetch('https://dummyjson.com/quotes/random')
        .then(res => res.json())
        .then(data => {
            currentQuote.value = {
                text: data.quote,
                author: data.author
            }
        })
        .catch(error => {
            console.error('Error fetching quote:', error)
        })
}
onMounted(getRandomQuote())



</script>

<style>

.quote-generator {
  max-width: 400px;
  margin: 50px auto;
  padding: 20px;
  text-align: center;
  border: 1px solid #ccc;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.app-title {
  font-size: 24px;
  margin-bottom: 20px;
  color: #333;
}

.quote-container {
  background-color: #f9f9f9;
  padding: 20px;
  border-radius: 8px;
  border: 1px solid #ddd;
  margin-bottom: 20px;
}

p {
  font-size: 18px;
  margin-bottom: 10px;
}

cite {
  font-style: normal;
  color: #777;
}

.quote-button {
  padding: 10px 20px;
  font-size: 16px;
  background-color: #3498db;
  color: #fff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.quote-button:hover {
  background-color: #2980b9;
}
</style>
