<template>
  <div class="divination">
    <div class="divination-logo">
      <img src="../assets/logo.gif" alt="" />
    </div>
    <div class="divination-content">
      <div class="divination-inputText">
        我要抽
        <input
          class="divination-input"
          v-model="inputCardNum"
          @blur="checkInput"
          type="number"
          max="48"
          min="1"
          placeholder="?"
        />張牌
      </div>
      <button class="divination-button" @click="showDialog">開始抽牌</button>
      <div class="divination-notification">✦抽完牌請截圖回傳✦</div>
      <div
        class="divination-result"
        :class="{ mobile: cardResult.length <= 3 }"
      >
        <div
          class="divination-result-imgBox"
          v-for="card in cardResult"
          :key="card"
        >
          <img class="divination-result-img" :src="getImgUrl(card)" alt="" />
        </div>
      </div>
      <div class="divination-footer">
        <div class="divination-footerBox">
          <a :href="socialMedia.youtube">
            <img
              class="socialMedia-link"
              src="../assets/socialMedia/icon-yt.png"
              alt=""
            /> </a
          ><a :href="socialMedia.twitter">
            <img
              class="socialMedia-link"
              src="../assets/socialMedia/icon-tw.png"
              alt=""
            />
          </a>
          <a :href="socialMedia.facebook">
            <img
              class="socialMedia-link"
              src="../assets/socialMedia/icon-fb.png"
              alt=""
            />
          </a>
        </div>
      </div>
    </div>
    <q-dialog
      v-model="isDialogShow"
      persistent
      transition-show="flip-down"
      transition-hide="flip-up"
    >
      <q-card class="divination-dialog">
        <q-card-section>
          <div>請心中請想著問題</div>
          <div>(有指定對象或事物也請一起想著)</div>
          <div>想完之後請按下【抽起來】</div>
        </q-card-section>
        <q-card-actions align="right">
          <q-btn label="再想想" color="primary" v-close-popup />
          <q-btn
            label="抽起來"
            color="primary"
            @click="randomPick"
            v-close-popup
          />
        </q-card-actions>
      </q-card>
    </q-dialog>
  </div>
</template>

<script>
export default {
  name: "TheDivination",
  data() {
    return {
      inputCardNum: 3,
      isDialogShow: false,
      cardResult: [],
      socialMedia: {
        youtube: "https://www.youtube.com/channel/UCXqEvZGP5_KWzD6nCSSCUsQ",
        facebook: "https://www.facebook.com/profile.php?id=100084147997702",
        twitter: "https://twitter.com/OoniauNuannuan",
      },
    };
  },
  methods: {
    showDialog() {
      this.isDialogShow = true;
    },
    checkInput() {
      if (this.inputCardNum > 48) {
        this.inputCardNum = 48;
      }
      if (this.inputCardNum < 1) {
        this.inputCardNum = 1;
      }
    },
    randomPick() {
      this.cardResult = [];

      let arr = [
        1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20,
        21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38,
        39, 40, 41, 42, 43, 44, 45, 46, 47, 48,
      ];
      let result = [];

      for (let i = 0; i < this.inputCardNum; i++) {
        const rand = Math.floor(Math.random() * arr.length);

        result.push(arr[rand]);
        arr.splice(rand, 1);
      }

      this.cardResult = result;
    },
    getImgUrl(pic) {
      return require("../assets/divination-card/" + pic + ".jpg");
    },
  },
  computed: {
    isColumn() {
      if (this.cardResult.length <= 3) {
        return "column";
      }
      return "row";
    },
  },
};
</script>

<style lang="scss" scoped>
.divination {
  overflow-x: hidden;
  margin-top: 30px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;

  .divination-logo {
    display: flex;
    justify-content: center;
    align-items: center;

    img {
      max-width: 20%;
      overflow: hidden;
    }
  }

  .divination-content {
    margin-top: 30px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;

    .divination-inputText {
      display: flex;
      color: #f5d269;
      font-weight: bold;
      font-size: 1.5rem;

      .divination-input {
        text-align: center;
        width: 60px;
        font-size: 1.5rem;
        font-weight: normal;
        border-radius: 5px;
        border: 1px solid black;
        margin: 0 5px;
      }
    }
  }

  .divination-button {
    margin-top: 20px;
    width: 200px;
    font-size: 2rem;
    letter-spacing: 8px;
    border-radius: 20px;
    border: none;
    color: white;
    background-color: #f5d269;
    cursor: pointer;
  }

  .divination-result {
    margin: 10px 0 60px;
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    flex-wrap: wrap;

    .divination-result-imgBox {
      margin: 5px;
      display: flex;
      justify-content: center;
      align-items: center;
      width: 100%;
      max-width: 30% !important;

      .divination-result-img {
        width: 100%;
      }
    }
  }
}

.divination-dialog {
  width: 70%;
  font-size: 16px;
  color: #7f7093;
  text-align: center;

  .q-card__actions > button {
    background-color: #f5d269 !important;
  }
}

.divination-notification {
  margin-top: 10px;
  font-size: 24px;
  font-weight: bold;
  color: #f5d269;
}

.divination-footer {
  position: fixed;
  left: 0;
  bottom: 0;
  width: 100%;
  height: 50px;
  background-color: #d3cbe7;
  display: flex;
  justify-content: center;
  align-items: center;

  .divination-footerBox {
    margin-top: 6px;
  }
}

.socialMedia-link {
  width: 35px;
  height: 35px;
  margin: 0 10px;
}

@media screen and (max-width: 1200px) {
  .divination {
    .divination-logo {
      img {
        max-width: 35%;
      }
    }
  }
}

@media screen and (max-width: 900px) {
  .divination {
    .divination-logo {
      img {
        max-width: 40%;
      }
    }
  }
}

@media screen and (max-width: 450px) {
  .divination {
    .divination-logo {
      img {
        max-width: 60%;
      }
    }
  }

  .divination-dialog {
    width: 80%;
    font-size: 14px;
  }
}
</style>
