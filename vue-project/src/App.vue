<script setup>
import { ref } from "vue";
import axios from "axios";

const key = 

document.getElementById("getbutton").addEventListener("click", getmovie);

function getmovie() {
  let movieId = parseInt(document.getElementById("list").value);

  let search = axios.get("https://api.themoviedb.org/3/movie/" + movieId, {
    params: {
      api_key: key,
      append_to_response: "videos",
    },
  });

  search.then((movieData) => {
    document.getElementById("poster").src =
      "https://image.tmdb.org/t/p/w500" + movieData.data.poster_path;

    document.getElementById("title").innerHTML = movieData.data.original_title;
    document.getElementById("tagline").innerHTML = movieData.data.tagline;
    document.getElementById(
      "status"
    ).innerHTML = `${movieData.data.status}: ${movieData.data.release_date}`;
    document.getElementById(
      "language"
    ).innerHTML = `Languages: ${movieData.data.language}`;
    document.getElementById(
      "runtime"
    ).innerHTML = `Run-time: ${movieData.data.runtime} minutes`;
    document.getElementById(
      "popularity"
    ).innerHTML = `Popularity: ${movieData.data.popularity}`;
    document.getElementById(
      "voteAverage"
    ).innerHTML = `Vote Average: ${movieData.data.vote_average}`;
    document.getElementById(
      "voteCount"
    ).innerHTML = `Vote Count: ${movieData.data.vote_count}`;
    document.getElementById(
      "budget"
    ).innerHTML = `Budget: $${movieData.data.budget}`;
    document.getElementById("overview").innerHTML = movieData.data.overview;
    document.getElementById("trailer").src =
      "https://www.youtube.com/embed/" +
      movieData.data.videos.results
        .filter((trailer) => trailer.type === "Trailer")
        .at(0).key;
  });
}

</script>

<template>
  <head>
    <div id="pagetop">
      <select id="list" name="Select">
        <option value="809">Shrek 2</option>
        <option value="76600">Avatar: The Way of Water</option>
        <option value="505642">Black Panther: Wakanda Forever</option>
        <option value="502356">The Super Mario Bros. Movie</option>
        <option value="594767">Shazam! Fury of the Gods</option>
        <option value="603692">John Wick: Chapter 4</option>
        <option value="640146">Ant-Man and the Wasp: Quantumania</option>
        <option value="378064">A Silent Voice: The Movie</option>
        <option value="2109">Rush Hour</option>
        <option value="9502">Kung Fu Panda</option>
      </select>
      <button id="getbutton">Get</button>
    </div>
  </head>


  <body>
    <div class="container">
      <div id="containertop">
        <div id="left">
          <img id="poster" src="" />
        </div>
        <div id="right">
          <h1 id="title"></h1>
          <h3 id="tagline"></h3>
          <p id="overview"></p>
        </div>
      </div>
      <div id="containerbot">
        <h3 id="status"></h3>
        <p id="language"></p>
        <p id="runtime"></p>
        <p id="popularity"></p>
        <p id="voteAverage"></p>
        <p id="voteCount"></p>
        <p id="budget"></p>
      </div>
      <iframe id="trailer"></iframe>
    </div>
  </body>
</template>

<style scoped>
* {
  font-family: "Poppins", sans-serif;
  padding: 0;
  margin: 5px;
  box-sizing: border-box;
  background-color: rgb(24, 23, 23);
}

.container {
  margin-top: 20px;
  width: 100%;
  align-items: center;
}

#pagetop {
  display: flex;
  margin-left: auto;
  margin-right: auto;
  margin-top: 20px;
  text-align: center;
  width: 20%;
  height: 40px;
}

#list {
  color: azure;
  border-radius: 5px;
}

#getbutton {
  margin-left: 5px;
  color: azure;
  border-radius: 5px;
}

#containertop {
  height: 100vh;
  width: 100%;
  justify-content: space-between;
  display: flex;
}

.left {
  width: 40%;
}

img {
  border-radius: 8px;
}

.right {
  width: 55%;
}

h1 {
  color: rgb(225, 218, 218);
  font-size: 60px;
}

h3 {
  color: rgb(175, 169, 169);
  font-size: 35px;
}

p {
  color: rgb(158, 156, 156);
  font-size: 20px;
}

#containerbot {
  overflow: hidden;
  width: 100%;
}

iframe {
  bottom: 0px;
  float: right;
  border-radius: 8px;
  position: sticky;
  aspect-ratio: 16/9;
  width: 50%;
}
</style>
