<template>
    <div class="grid">
      <div class="grid__left-bar bordered">
        <div class="left-bar-header bordered-sm">
          <img class="avatar" src="./assets/images/image-jeremy.png">
          <p class="font-sm">Report for</p>
          <h1>Damien</h1>
          <h1>Clairat</h1>
        </div>

        <div class="time-button-wrap font-md">
          <label class="radio-text" for="daily">
            <input type="radio" name="time-button" id="daily"
                   v-model="timeFrame" value="daily" checked>
            <span>Daily</span>
          </label>
          <label class="radio-text" for="weekly">
            <input type="radio" name="time-button" id="weekly"
                   v-model="timeFrame" value="weekly">
            <span>Weekly</span>
          </label>
          <label class="radio-text" for="monthly">
            <input type="radio" name="time-button" id="monthly"
                   v-model="timeFrame" value="monthly">
            <span>Monthly</span>
          </label>
        </div>
      </div>

      <div class="grid__item-list">
        <template v-for="(theme,index) in timeData" :key="index">
          <div class="item-theme bordered" :class="trimSmall(theme.title)">
            <div class="item__header">
              <img :src="`src/assets/images/icon-${trimSmall(theme.title)}.svg`">
            </div>
            <div class="item__footer bordered-sm">
              <div class="item__lead">
                <h2 class="font-md">{{ theme.title }}</h2>
                <button>
                  <img src="./assets/images/icon-ellipsis.svg">
                </button>
              </div>
              <div class="current-hours font-xl">
                {{ theme.timeframes[timeFrame].current + " hrs" }}
              </div>
              <div class="previous-hours font-sm">
                <span>{{  getPreviousFrameText
                          + theme.timeframes[timeFrame].previous
                          + " hrs"}}</span>
              </div>
            </div>
          </div>
        </template>
      </div>
    </div>
</template>

<script>
import json from "../data.json";

export default{
  data(){
    return{
      timeData: json,
      timeFrame: "daily",
    }
  },
  methods: {
    trimSmall(text) {
      return text.replace(' ','').toLowerCase();
    }
  },
  computed: {
    getPreviousFrameText() {
      switch(this.timeFrame){
        case 'daily':
          return "Yesterday - ";
        case 'weekly':
          return "Last week - ";
        case 'monthly':
          return "Last month - ";
      }
    }
  }
}

</script>
