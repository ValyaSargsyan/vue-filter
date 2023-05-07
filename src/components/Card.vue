<script setup>
import CheckBoxField from './CheckboxField.vue'

defineProps({
    data: Object,
})

</script>

<template>
    <div class="card">
      <CheckBoxField v-model="data.selected" />
      <div class="card-content">
        <div class="card-content_left">
          <div>
            <div class="card-top">
              <span class="price">{{data.price}}</span>
              <div v-if="data.type === 'apartment'" class="type">
                <div class="type-content">
                  <img src="../assets/images/apartment.svg" alt="apartment">
                  <span class="type-text">Квартира</span>
                </div>
                <div class="tooltip">{{data.tooltipText}}</div>
              </div>
              <div v-else-if="data.type === 'parking'" class="type">
                <div class="type-content">
                  <img src="../assets/images/parking.svg" alt="parking">
                  <span class="type-text">Паркинг</span>
                </div>
                <div class="tooltip">{{data.tooltipText}}</div>
              </div>
            </div>
            <p class="quarter-frame">
              <span class="quarter">{{data.quarter}}</span>,
              <span class="frame">{{data.frame}}</span>
            </p>
          </div>
          <div class="info-wrap">
            <div>
              <p class="info-text">{{data.number}}</p>
              <p class="info-text">{{data.room}}</p>
            </div>
            <div class="size-info">
              <p class="info-text">{{data.size}}</p>
              <p class="info-text">{{data.floor}}</p>
            </div>
          </div>
          <div class="address">
            <img src="../assets/images/location.svg" alt="location">
            <div class="info-text">{{data.address}}</div>
          </div>
        </div>
        <div class="card-content_right">
          <div class="status" :class="data.status.type">
            <div class="circle"></div>
            <div class="status-text">{{data.status.text}}</div>
          </div>
          <div class="card-img">
            <img
                :src="data.image"
                alt="scheme"
            >
          </div>
          <div class="date">
            <span>Добавлено</span>
            <span>{{data.date}}</span>
          </div>
        </div>
      </div>
    </div>
</template>

<style scoped>
.card {
  display: flex;
  align-items: center;
  background: #FFFFFF;
  border: 1px solid #E5E5E5;
  padding: 20px 35px 25px;
  width: 100%;
  height: 240px;
}

.card-content {
  display: flex;
  justify-content: space-between;
  width: 100%;
  height: 100%;
  margin-left: 35px;
}
.card-top {
  width: 100%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 3px;
}
.price {
  font-family: 'PtSans-Bold', sans-serif;
  font-weight: 700;
  font-size: 15px;
  line-height: 20px;
  color: #FF0D29;
}
.type {
  position: relative;
  padding: 5px 16px;
  margin-left: 16px;
  background: #FFFFFF;
  box-shadow: 0 0 2px rgba(94, 119, 157, 0.25);
  border-radius: 32px;
  cursor: pointer;
  transition: .3s;
}
.type:hover .tooltip{
  display: block;
}
.tooltip {
  display: none;
  width: max-content;
  font-size: 12px;
  padding: 5px 10px;
  position: absolute;
  left: 20px;
  bottom: -35px;
  background: rgba(0, 0, 0, 0.8);
  color: #FFFFFF;
  box-shadow: 0 8px 30px -3px rgba(26, 32, 44, 0.1), 0 4px 6px -2px rgba(26, 32, 44, 0.05);
  transition: .3s;
}
.tooltip::after {
  content: " ";
  position: absolute;
  bottom: 100%;  /* At the top of the tooltip */
  left: 20px;
  margin-left: -5px;
  border-width: 5px;
  border-style: solid;
  border-color: transparent transparent  rgba(0, 0, 0, 0.8) transparent;
}
.type-content {
  display: flex;
  align-items: center;
}
.type-text {
  font-weight: 400;
  font-size: 12px;
  line-height: 16px;
  color: #232735;
  margin-left: 8px;
}
.quarter-frame {
  font-weight: 400;
  font-size: 14px;
  line-height: 150%;
}
.quarter-frame span:first-child {
  color: #000000;
}
.quarter-frame span:last-child {
  color: #808080;
}
.card-content_left {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  max-width: 300px;
}
.info-wrap {
  display: flex;
}
.info-text {
  font-weight: 400;
  font-size: 14px;
  line-height: 25px;
  color: #000000;
}
.address {
  display: flex;
  align-items: flex-start;
}
.address img {
  margin: 8px 11px 0 -25px;
}
.size-info {
  border-left: 1px solid #C4C4C4;
  padding-left: 28px;
  margin-left: 60px;
}

.card-content_right {
  display: flex;
  flex-direction: column;
  align-items: flex-end;
  margin-left: 20px;
}

.status {
  width: fit-content;
  padding: 6px 9px;
  display: flex;
  align-items: center;
  margin-bottom: 27px;
}

.legal-face {
  background: #FFE4E4;
  color: #DD4C5D;
}
.legal-face .circle {
  background: #DD4C5D;
}
.physical-face {
  background: #D6F5FF;
  color: #0291C1;
}
.physical-face .circle {
  background: #0291C1;
}
.reserved {
  background: #EDEDED;
  color: #686868;
}
.reserved .circle {
  background: #686868;
}
.sold {
  background: #CCCCCC;
  color: #808080;
}
.sold .circle {
  background: #808080;
}

.circle {
  width: 6px;
  height: 6px;
  border-radius: 50%;
  margin-right: 8px;
}

.status-text {
  font-weight: 400;
  font-size: 14px;
  line-height: 18px;
}

.date {
  width: 100%;
  display: flex;
  justify-content: space-between;
  font-weight: 400;
  font-size: 13px;
  line-height: 20px;
  color: #9B9B9B;
  margin-top: 12px;
}

.card-img img {
  width: 100%;
  height: 100%;
}

@media(max-width: 1400px) {
  .card-img {
    width: 120px;
    height: auto;
  }
}

@media(max-width: 1280px) {
  .card-content {
    margin-left: 25px;
  }
  .card {
    padding: 20px 0 25px 25px;
  }
  .card-content_left {
    max-width: 250px;
  }
  .card-img, .date {
    margin-right: 20px;
  }
}

@media(max-width: 550px) {
  .card {
    height: auto
  }
  .card-content {
    flex-direction: column-reverse;
    align-items: center;
  }
  .card-content_right {
    margin: 0 auto 10px;
  }
  .card-content_left {
    max-width: 100%;
    margin-right: 20px;
  }
  .card-top {
    flex-direction: column-reverse;
    justify-content: flex-start;
    align-items: flex-start;
  }
  .type {
    margin-left: 0;
    margin-bottom: 10px;
  }
}
</style>
