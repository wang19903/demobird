<template>
  <div class="container">
    <main>
      <Menu />
      <div class="rightContainer">
        <div class="bannerContainer">
          <img src="../assets/banner.svg" alt="白頭翁的圖片。Chinese bulbul's picture." />
          <div class="bannerDescript">
            <h3>白頭翁 (Chinese bulbul)</h3>
            <p>又名白頭鵯。以果實、昆蟲為主食，無法消化小米、穀類。平均壽命約 8~10 年。</p>
          </div>
        </div>
        <CardList />
      </div>
    </main>
    <!-- <Footer/> -->
  </div>
</template>

<script setup lang="ts">
// import Footer from './Footer.vue'
import CardList from './CardList.vue'
import Menu from './Menu.vue'
</script>

<style lang="scss" scoped>
//最外層設定直向排版、延伸到底，footer就可以置底
.container {
  display: flex;
  min-height: 100vh;
  flex-direction: column;
  justify-content: space-between;
  width: 100%;
  max-width: 1440px;
  overflow-x: hidden;
}

//設計稿寬1440px和375px，作為最大寬度和最小寬度
main {
  max-width: 1440px;
  min-width: 375px;
  margin: 0 auto;
  display: flex;
  justify-content: center;
  flex: 1;
  width: 100%;
}

.rightContainer {
  flex: 1.7;
  max-width: 1095px;
  display: flex;
  flex-direction: column;
  background-color: #DCCCBC
}

.bannerContainer {
  position: relative;

  img {
    width: 100%;
    min-height: 311px; //figma 行動版增高
    object-fit: cover;
    object-position: center;
  }


  h3 {
    font-style: normal;
    font-weight: 700;
    font-size: 48px;
    line-height: 65px;
    color: #fff;
    text-align: right;
    margin: 0;
  }

  .bannerDescript {
    position: absolute;
    bottom: 0;
    right: 0;
    margin: 1.3rem;
  }

  p {
    color: #fff;
    margin: 0;
    font-style: normal;
    font-weight: 400;
    font-size: 18px;
    line-height: 25px;
    text-align: right;
  }
}

@media (max-width: 768px) {
  main {
    flex-direction: column;
  }
}

@media (max-width: 480px) {
  .bannerContainer {
    img {
      object-position: -3rem center;
    }
  }
}
</style>
