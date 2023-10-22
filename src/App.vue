<template>
        <div class="header-content">
            <div class="logo">
              <img src="@/assets/codebusters.jpg" alt="Company Logo" width="100" height="100">
            </div>
            <div class="company-name">
                CodeBusters
            </div>
        </div>
  <router-view/>
</template>

<style>
@font-face {
  font-family: "bebas";
  src: url('@/assets/Bebas_Neue/BebasNeue-Regular.ttf');
}

#app{
  align-items: center;
  margin: 0 !important;
  font-family: bebas;
  background-color: #130f2a;
}

.header-content {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  background-color: #130f2a;
}
</style>
