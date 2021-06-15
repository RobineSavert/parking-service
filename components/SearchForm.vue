<template>
  <div>
    <b-row>
      <b-col>
        <b-jumbotron header="Search a parking" lead="Here you can find a parking" class="bg-white mt-4">
          <b-form>

            <label for="dateFrom" class="mr-sm-2">From</label>
            <b-form-datepicker id="dateFrom" v-model="valueFrom" class="mb-2 mr-sm-4 mb-sm-0 w-100" :min="min" :max="max"></b-form-datepicker>

            <label for="dateTo" class="mr-sm-2">To</label>
            <b-form-datepicker id="dateTo" v-model="valueTo" class="mb-2 mr-sm-4 mb-sm-0 w-100" :min="min" :max="max"></b-form-datepicker>

            <b-button variant="primary" @click="$fetch()" class="mt-4">Search</b-button>

          </b-form>
        </b-jumbotron>
      </b-col>
    </b-row>

    <Loader v-if="$fetchState.pending" />

    <Alert v-else-if="$fetchState.error" />

   <Results :items="items" v-else />

  </div>
</template>
<script>
export default {
  data() {
    const now = new Date();
    const today = new Date(now.getFullYear(), now.getMonth(), now.getDate());
    const minDate = new Date(today);
    const maxDate = new Date(today);
    maxDate.setMonth(maxDate.getMonth() + 6);
    return {
      items: {},
      valueFrom: '',
      valueTo: '',
      min: minDate.toISOString(),
      max: maxDate.toISOString()
    }
  },
  async fetch() {
    try {
      const api = `https://parkos.nl/ajax/locationSearchJSON/?location=parkeren-schiphol&arrival=${this.valueFrom}&arrivalTime=12%3A00&departure=${this.valueTo}&departureTime=12%3A00&sort_f=price&sort_w=asc`
      this.items = await fetch(api).then(res => res.json())
    } catch (error){
      console.error(error.message);
    }
  }
}
</script>
<style>
  h1 {
    font-size: 80%;
  }

  .btn-primary {
    background-color: #17a2b8 !important; /* 100/100 would NOT do this in real life guys!!!! im actually embarrassed! */
    border-color: #17a2b8 !important;
  }
</style>
