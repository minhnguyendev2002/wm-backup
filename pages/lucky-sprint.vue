<template>
    <div>
        <div class="w-[475px] h-[80vh] relative mx-auto mt-5 mb-5 rounded-md px-3 py-5 bg-[#fff]" style="box-shadow: rgba(0, 0, 0, 0.18) 0px 2px 4px;">
            <h1 class="text-center text-[30px] font-bold uppercase  text-[#ffd212]">
                Lucky Sprint
            </h1>
            <div>
                <a-radio-group v-model="type" @change="(e) => type = e.target.value">
                    <a-radio :value="1">
                        Chọn số
                    </a-radio>
                    <a-radio :value="2">
                        Nhập số
                    </a-radio>
                </a-radio-group>
            </div>
            <a-select
                v-if="type === 2"
                :v-model="value"
                mode="tags"
                style="width: 100%; margin-top:20px"
                :token-separators="[',']"
                placeholder="Nhập số random"
                :options="options"
                class="mt-5"
                @change="handleChange"
            />
            <div class="grid grid-cols-1 gap-3 mt-5 number-random">
                <div class="button button-dial">
                    <span class="button-dial-spoke" />
                    <span class="button-dial-spoke" />
                    <span class="button-dial-spoke" />
                    <span class="button-dial-spoke" />
                    <span class="button-dial-spoke" />
                    <span class="button-dial-spoke" />

                    <div class="button-dial-top" />
                    <div class="button-dial-label">
                        <h1 class="m-0  text-[45px] font-semibold text-[#067CF8]">
                            {{ formatNumber(number) }}
                        </h1>
                    </div>
                </div>
            </div>
            <div class="flex items-center justify-around absolute !bottom-[30px] w-full">
                <button class="button" @click="start">
                    Quay số
                </button>
            </div>
        </div>
    </div>
</template>

<script>

    export default {
        scrollToTop: true,
        components: {
        },

        data() {
            return {
                loading: false,
                number: Math.floor(Math.random() * 100),
                status: false,
                options: [],
                type: 1,
            };
        },
        mounted() {
            const countDown = setInterval(() => {
                if (true) {
                    // this.start();
                }
                // if (seconds === 0) {
                // if (minutes === 0) {
                // clearInterval(countDown);
                // } else {
                // this.start();
                // }
                // }
            }, 200);
            return () => {
                clearInterval(countDown);
            };
        },

        methods: {
            start() {
                const countDown = setInterval(() => {
                    this.number = Math.floor(Math.random() * 100);
                    this.$forceUpdate();
                }, 50);
                setTimeout(() => {
                    clearInterval(countDown);
                }, 3000);
            },
            formatNumber(number) {
                return number < 10 ? `0${number}` : number;
            },
            handleChange(value) {
                console.log(value);
            },
        },

        head() {
            return {
                title: 'Về chúng tôi',
            };
        },
    };
</script>

<style lang="scss">
    button {
    all: unset;
    display: inline-block;
    padding: 10px 20px;
    color: white;
    text-transform: uppercase;
    font-family: sans-serif;
    letter-spacing: 1.5px;
    font-weight: bold;
    cursor: pointer;
    border-radius: 17px;
    }

    .button {
        background-color: #58cc02;
        box-shadow: 0 5px 0 #58a700;
        width: 120px;
        text-align: center;
    }

    .button:active {
    box-shadow: none;
    transform: translateY(5px);
    }
    .ant-radio-inner::after {
        top: 3.2px !important
    }
    @keyframes bounce {
    from {
      transform: translateY(360px);
      transition: all .1s ease-in-out;
      opacity: 1;
    }
    to {
      opacity: 1;
      transition: all .1s ease-in-out;
      transform: translateY(-360px);
    }
  }
  @keyframes fade {
  0% {
      opacity: 0;
      transition: all .1s ease-in-out;
  }
  100% {
      opacity: 1;
      transition: all .1s ease-in-out;
  }
}

  p {
    animation: fade 200ms infinite
  }
  .number-random {
 *,
*:before,
*:after {
  box-sizing: inherit;
}

body {
  background-color: #f2f2f2;
}

.color-cool {
  color: #077dfe;
}

.color-warm {
  color: #ff7a00;
}

.container {
  display: flex;
  justify-content: space-evenly;
  padding-top: 25px;
  align-items: center;
  flex-direction: column;
}

@media screen and (min-width:800px) {
  .container {
    flex-direction: row;
  }
}

.app-container {
  background-color: var(--bg-color);
  border-radius: 40px;
  box-shadow: -2px -2px 4px 0px #ffffff, 50px 50px 50px 0px rgba(0, 0, 0, .25);
  display: block;
  flex: 1;
  min-height: 500px;
  max-width: 350px;
  margin-bottom: 25px;
  overflow: hidden;
  padding: 30px;
}

.app-top-bar {
  display: flex;
  align-items: center;
  margin-bottom: 30px;
}

.app-heading {
  color:#222;
  display: block;
  flex: 1;
  font-size: 28px;
  font-weight: 800;
  margin: 0;
  text-align: center;
}

button {
border: 0;
&:focus {
border: none;
outline: 0 !important;
outline-style: none;
}
}

.button {
  color: #222;
  position: relative;
  border-radius: 15px;
  background:  #f2f3f7;
  font-weight: 700;
  transition: all 100ms cubic-bezier(0.175, 0.885, 0.32, 1.275);
  box-shadow: -6px -6px 8px rgba(255, 255, 255, 0.9),
    5px 5px 8px rgba(0, 0, 0, 0.07);
  cursor: pointer;
  &.button-link {
    color: #067CF8;
    display: block;
    font-size: 17px;
    margin: 30px 0 0;
    padding: 20px 0;
    width: 100%;
  }
  &.button-small {
    color: #6D6E74;
    font-size: 22px;
    line-height: 40px;
    width: 40px;
    height: 40px;
  }
  &.button-large {
    display: flex;
    font-size: 20px;
    flex-direction: column;
    padding: 15px;
    text-align: left;
    width: 45%;
    & svg {
      margin-bottom: 40px;
      width: 30px;
    }
  }
}
.button-dial {
  border-radius: 50%;
  display: flex;
  height: 270px;
  margin: 35px auto;
  align-items: center;
  justify-content: center;
  width: 270px;
}

.button-dial-top {
  background: #f2f3f7;
  box-shadow:  -6px -6px 8px rgba(255, 255, 255, 0.9),
    5px 5px 8px rgba(0, 0, 0, 0.07);
  border-radius: 50%;
  width: 70%;
  height: 70%;
  margin: 0 auto;
  position: absolute;
  top: 15%;
  left: 15%;
  text-align: center;
  z-index: 5;
}

.button-dial-label {
  color: #067CF8;
  font-size: 28px;
  fill: #067CF8;
  position: relative;
  z-index: 10;
}

.button-dial-spoke {
  background-color: rgba(96, 171, 254, 0.6);
  display: block;
  height: 2px;
  width: 83%;
  position: absolute;
  margin: 0 auto;
  z-index: 5;
  top: 50%;
  &:nth-child(2) {
    transform: rotate(30deg);
  }
  &:nth-child(3) {
    transform: rotate(60deg);
  }
  &:nth-child(4) {
    transform: rotate(90deg);
  }
  &:nth-child(5) {
    transform: rotate(120deg);
  }
  &:nth-child(6) {
    transform: rotate(150deg);
  }
}

.button-block {
  align-items: center;
  display: flex;
  justify-content: space-between;
  padding: 15px 24px;
  width: 100%;
  span {
    font-size: 16px;
  }
}

.subtle {
  color: #6D6E74;
}

.flex-button-container {
  display: flex;
  justify-content: space-between;
}
.ant-select-dropdown.ant-select-dropdown--multiple .ant-select-dropdown-menu-item {
    background: #067CF8 !important;
}
  }
</style>
