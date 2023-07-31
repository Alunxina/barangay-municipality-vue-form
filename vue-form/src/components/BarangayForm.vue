<template>
  <div>
    <div class="container">
      <div class="card">
        <div class="columns">
          <div class="column">
            <h1 class="title has-text-left pb-3 pb-3">
              <strong>Fetch Barangay</strong>
            </h1>
            <h2 class="has-text-left pb-3">
              Use this in order to find a list of barangays with the province
              and municipality. The input is case sensitive so make sure that
              your capitalizations are correct.
            </h2>
          </div>
          <div class="column">
            <form @submit.prevent="fetchData">
              <div class="column has-text-left is-size-5">
                <label for="province">Province: </label>
                <input
                  v-model="province"
                  type="text"
                  id="province"
                  required
                  class="input"
                />
              </div>
              <div class="column has-text-left is-size-5">
                <label for="municipality">Municipality: </label>
                <input
                  v-model="municipality"
                  type="text"
                  id="municipality"
                  required
                  class="input"
                />
              </div>
              <div class="column has-text-left is-size-7">
                <button type="submit" class="button is-link is-small">
                  Fetch Barangay
                </button>
              </div>
            </form>
          </div>
        </div>
      </div>

      <!-- Title of the list -->
      <h3 v-if="showTitle" class="title has-text-left pb-3 pt-5">
        List of Barangays in {{ municipalityToShow }}:
      </h3>

      <div class="columns is-multiline">
        <div class="column is-3" v-for="barangay in barangays" :key="barangay">
          <div class="box has-text-centered pb-3">
            {{ barangay }}
          </div>
        </div>
      </div>

      <!-- No results message -->
      <div class="card title" v-if="error == true && barangays.length === 0">
        <p>No barangays found.</p>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      province: '',
      municipality: '',
      barangays: [],
      municipalityToShow: '',
      error: false, // Add a new data property to track errors
      showTitle: false
    };
  },
  methods: {
    async fetchData() {
      console.log('Fetching data...');

      try {
        const url = `https://demo.myruntime.com/website/fulfillmentClustersService/api/getPhilClusterOptions/myruntimeWeb?parentOption=${encodeURIComponent(
          this.province
        )}&childOption=${encodeURIComponent(this.municipality)}`;

        const response = await axios.get(url);
        this.barangays = response.data.data;
        this.error = false; // Reset error state when fetch is successful
        this.showTitle = true;
        this.municipalityToShow = this.municipality;

        console.log('API Response:', this.barangays);
      } catch (error) {
        console.error('Error fetching data:', error);
        this.barangays = [];
        this.error = true;
        this.showTitle = false;
      }
    }
  }
};
</script>
<style scoped>
@import '~bulma/css/bulma.css';
@import url('https://fonts.googleapis.com/css2?family=Palanquin&family=REM&display=swap');
.title {
  font-family: 'Palanquin', sans-serif;
}
.container {
  overflow-y: hidden;
  overflow-x: hidden;
  padding-bottom: 5rem;
}

.column {
  font-family: 'Palanquin', sans-serif;
}
.input {
  width: 200px;
  height: 40px;
  border-radius: 5px;
  border: 2px solid #323232;
  background-color: #fff;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
  font-size: 15px;
  font-weight: 600;
  color: #323232;
  padding: 5px 10px;
  outline: none;
  font-family: 'Palanquin', sans-serif;
}

.input::placeholder {
  color: #666;
  opacity: 0.8;
}

.input:focus {
  border: 2px solid #2d8cf0;
}

@media screen and (min-width: 280px) and (max-width: 1180px) {
  .container {
    padding-left: 3rem;
    padding-right: 3rem;
  }

  .column {
    padding-left: 1rem;
    padding-right: 1rem;
    justify-content: center;
    width: auto;
  }
  .button {
    width: 100%;
  }
}
</style>
