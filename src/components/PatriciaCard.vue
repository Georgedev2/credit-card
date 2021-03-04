<template>
  <div>
    <div class="credit-card">
      <div>
        <div class="credit-card_1st-child">
          <div class="card_logo_">
            <img src="../assets/patricia-logo.png" alt="" />
          </div>
          <!-- THE EYE BUTTONS AT THE TOP OF THE RIGHT CORNER -->
          <div class="credit-card_eye">
            <!-- THE BLIND EYE BUTTON  -->
            <img
              src="../assets/blind-eye-icon.png"
              alt="blind-eye"
              v-if="isBlind"
              @click="showCardDetails"
            />
            <!-- THE OPEN EYE BUTTON  -->
            <img
              src="../assets/open-eye-icon.png"
              alt="open-eye"
              v-else
              @click="holdCardDetails"
            />
          </div>
        </div>

        <!-- THE NUMBER AT THE MIDDLE OF THE CARD -->
        <ul class="card-num-box">
          <li
            v-for="({ cardNumber, isdisplayed }, idx) in cardNumbers"
            :key="idx"
          >
            <!-- CARD NUMBERS  -->
            <span v-if="isdisplayed" class="one-of-4-card-nums">
              {{ cardNumber }}</span
            >

            <ul class="an-ellipsis" v-else>
              <!-- THIS MARKUP WILL RETURNS AN ELLIPSIS EVERY TIME ITS PARENT FOR IN LOOP RUNS (...) -->
              <li class="dot" v-for="dot in dots" :key="dot"></li>
            </ul>
          </li>
        </ul>
        <!-- ADDITIONAL CARD INFORMATION AT THE BUTTON -->
        <div class="patricia-card_holder-info">
          <span class="card-name"> Cardholder Name </span>

          <div class="card-expriration">
            <div class="validity">
              <span>VALID</span>
              <span>THRU</span>
            </div>

            <span class="date">10/20</span>
            <span class="cvv">CVV</span>

            <div>
              <ul v-if="isBlind">
                <!-- THIS MARKUP WILL RETURNS AN ELLIPSIS. EACH OF THE list tag WILL RETURN A DOT(...) -->
                <li class="dot" v-for="dot in dots" :key="dot"></li>
              </ul>
              <span v-else style="color:#d3dce6;">
                7865
              </span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'PatriciaCard',
  data() {
    return {
      isBlind: true,
      cardNumbers: [
        {
          cardNumber: '4093',
          isdisplayed: false,
        },
        {
          cardNumber: '4983',
          isdisplayed: false,
        },
        {
          cardNumber: '4053',
          isdisplayed: false,
        },
        {
          cardNumber: '4353',
          isdisplayed: true,
        },
      ],
      dots: [1, 2, 3],
    };
  },

  methods: {
    showCardDetails() {
      this.cardNumbers = this.cardNumbers.map((el, idx, arr) => {
        if (idx === arr.length - 1) {
          return el;
        } else {
          el.isdisplayed = true;
          return el;
        }
      });
      this.isBlind = false;
    },
    holdCardDetails() {
      this.cardNumbers = this.cardNumbers.map((el, idx, arr) => {
        if (idx === arr.length - 1) {
          el.isdisplayed = true;
          return el;
        } else {
          el.isdisplayed = false;
          return el;
        }
      });
      this.isBlind = true;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
* {
  margin: 0;
  padding: 0;
}

.credit-card {
  width: 500px;
  height: 325px;
  background: #131313;
  border-radius: 20px;
  box-sizing: border-box;

  /* This Style will center the credit-card at the center of the document  */
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background-image: url('../assets/background-img.png');
  background-repeat: no-repeat;
}
.credit-card > div {
  width: 87%;
  height: 80%;
  display: flex;
  justify-content: space-between;
  flex-direction: column;

  /* This Style will center the credit-card first child  */
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

/*---- Styling of the credit-card first child which compreses of the credit-card logo and the credit-card eye ------*/
.credit-card_1st-child {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
}
.card_logo_ img {
  width: 95px;
  height: 16px;
}

/*------ Styling of the credit-card eye------ */
.credit-card_eye img {
  height: 23px;
  width: 25px;
  cursor: pointer;
}

.credit-card ul {
  list-style-type: none;
}
/*----- Styling of the numbers at the middle of the card---- */
.card-num-box {
  display: flex;
  justify-content: space-between;
}
.one-of-4-card-nums {
  font-size: 20px;
  color: #d3dce6;
  letter-spacing: 2px;
}

.an-ellipsis {
  font-size: 30px;
  color: #d3dce6;
  margin-top: -15px;
  list-style: none;
}

.dot {
  display: inline-block;
  width: 4.5px;
  height: 5px;
  background-color: #d3dce6;
  border-radius: 100%;
  margin: 3px;
  overflow: hidden;
}

/*-- Stlying of the card holder information----- */
.patricia-card_holder-info {
  display: flex;
  justify-content: space-between;
  color: #808080;
}
.card-name {
  font-size: 16px;
  color: #d3dce6;
}

.card-expriration {
  display: flex;
  justify-content: space-evenly;
}

.validity {
  display: flex;
  flex-direction: column;
  font-size: 6px;
  margin: 3px 5px;
}

.cvv {
  margin: 4px 10px 0px 40px;
  font-size: 8px;
}
.date {
  color: #d3dce6;
}
</style>
