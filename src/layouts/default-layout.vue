<template>
  <v-container>
    <main class="flex-fill d-flex flex-column py-5">
      <v-card
        class="d-flex flex-column"
        style="height: calc(100vh - 24px); overflow: hidden"
      >
        <header class="main-card-header">
          <div class="header-top d-flex">
            <div class="header-top-left text-left flex-grow-1 flex-shrink-0">
              <slot name="header-top-left"></slot>
            </div>
            <div
              class="header-top-right d-flex flex-column align-end justify-end"
            >
              <slot name="header-top-right"></slot>
            </div>
          </div>
          <div class="header-sub">
            <slot name="header-sub"></slot>
          </div>
        </header>

        <div class="card-body-wrapper flex-grow-1">
          <slot name="content"></slot>
        </div>
        <v-footer
          tag="footer"
          padless
          class="d-flex py-3 mt-auto justify-center"
        >
          <span class="font-weight-bold"> created by zzharuk </span>
        </v-footer>
      </v-card>
    </main>
  </v-container>
</template>

<script>
export default {
  name: "DefaultLayout",
};
</script>

<style lang="scss" >
main {
  max-width: 500px;
  height: 100vh;
  margin: 0 auto;
}

.card-body-wrapper {
  overflow: auto;
  &::-webkit-scrollbar {
    width: 10px;
  }

  &::-webkit-scrollbar-track {
    background-color: #cfcfcd;
  }

  &::-webkit-scrollbar-thumb {
    background-color: darkgrey;
  }
}
$base-grey-color: #a8a9ca;

header {
  background: linear-gradient(to bottom, #fff, #fafaff);
  border-bottom: 1px solid #e0e9f1;
  .header-top {
    padding: 30px;
    border-bottom: 1px solid #e0e9f1;
  }
  .header-top-left {
    .day {
      font-size: 30px;
      color: #666afb;
      letter-spacing: 0.8;
    }
    .month {
      display: block;
      margin-top: 15px;
      font-size: 20px;
      color: $base-grey-color;
      letter-spacing: 0.4;
    }
  }

  .input-field-task .v-input__slot {
    padding: 18px;
    font-size: 20px;
    .v-input__prepend-inner .v-icon {
      color: $base-grey-color;
      font-size: 34px;
    }
    .v-input__icon--prepend-inner {
      margin-right: 22px;
    }

    &::before {
      border-color: $base-grey-color !important;
      border-width: 2px 0 0 0;
    }
  }
}
</style>