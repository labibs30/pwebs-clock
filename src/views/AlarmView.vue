<template>
  <Navbar/>
    <div class="digital-clock">
        <!-- <i class="uil uil-ellipsis-v dot-menu-btn" id="active-menu"></i>
        <ul class="dot-menu" id="active-menu">
        <li class="menu-item" id="active-menu">
            <span class="clock-format-text" id="active-menu">24-hour format</span>
            <div class="format-switch-btn" data-format="12" id="active-menu"></div>
        </li>
        </ul> -->
        <div class="time">
            <span class="hours">{{displayHours}}</span>
            <span class="dots">:</span>
            <span class="minutes">{{displayMinutes}}</span>
            <div class="right-side">
                <span class="period">{{displayPeriod}}</span>
                <span class="seconds">{{displaySeconds}}</span>
            </div>
        </div>
        <form>
          <div class="form">
            <div class="nes-field">
               <input id="inputan" type="number" placeholder="Hour ..." name="hour" v-model="hour" class="h" max="23" min="00" required>
            </div>
            <div class="nes-field">
               <input id="inputan" type="number" placeholder="Minute ..." name="minute" v-model="minute" class="m" max="59" min="00" required>
            </div>
          </div>
        <button  type="text" @click="onClicked" id="button" class="set">Set Alarm</button>
        </form>
        
  </div>
</template>

<script>
import Navbar from "../components/Navbar.vue"
export default {
    name:'AlarmView',
    components:{
        Navbar
    },
    data(){
      var audio = new Audio(require('@/assets/ringtone.mp3'))
        return{
            displayHours: 0,
            displayMinutes: 0,
            displaySeconds: 0,
            displayPeriod: 0,
            isActive:false,
            minute:'',
            hour:'',
            audio:audio
        }
    },
    methods:{
        onClicked(){
          this.isActive = !this.isActive;
          if(this.isActive){
            console.log(this.hour, this.minute);
            document.querySelector(".h").disabled = true;
            document.querySelector(".m").disabled = true;
            document.querySelector(".set").innerHTML = "Clear Alarm"
          }else{
            document.querySelector(".h").disabled = false;
            document.querySelector(".m").disabled = false;
            this.hour = "",
            this.minute = "",
            document.querySelector(".set").innerHTML = "Set Alarm"
            this.audio.pause();
          }

          event.preventDefault();

        },
        clock(){
            const timer = setInterval(()=>{
                var today = new Date();
                var hours = today.getHours();
                var minutes = today.getMinutes();
                var seconds = today.getSeconds();

                let period = "AM";


                if(this.displayHours === this.hour && this.displayMinutes === this.minute){
                  this.audio.play();
                }
                console.log(this.hour, this.minute, this.displayHours, this.displayMinutes);
                this.displayHours = hours < 10 ? this.displayHours = "0"+ hours  : this.displayHours = hours;
                this.displayPeriod = hours >= 12 ? this.displayPeriod = "PM" : this.displayPeriod= period;
                this.displayMinutes = minutes < 10 ? this.displayMinutes = "0" + minutes: this.displayMinutes = minutes;
                this.displaySeconds = seconds < 10 ? this.displaySeconds = "0" + seconds: this.displaySeconds = seconds;


           }, 1000)
            
        }
    },
    mounted(){
      this.clock();

    }
}
</script>

<!-- <style>
@import url("https://fonts.googleapis.com/css2?family=Poppins:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&display=swap");

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Poppins", sans-serif;
}

body {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background: #2e2e44;
}

.digital-clock {
  position: relative;
  color: #fff;
  background: #2d2f41;
  width: 425px;
  padding: 20px 45px;
  box-shadow: 0 5px 25px rgba(14, 21, 37, 0.8);
  border-radius: 10px;
  display: flex;
  justify-content: center;
  align-items: center;
  display: flex;
  flex-direction: column;
}

.digital-clock::before {
  content: "";
  position: absolute;
  background: linear-gradient(45deg, #24ff6d, #2f93f1, #ff5e9a);
  background-size: 200% 200%;
  top: -5px;
  left: -5px;
  bottom: -5px;
  right: -5px;
  z-index: -1;
  filter: blur(40px);
  animation: glowing 10s infinite;
}

@keyframes glowing {
  0% {
    background-position: 0 50%;
  }
  50% {
    background-position: 100% 50%;
  }
  100% {
    background-position: 0 50%;
  }
}
.time {
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
}

.hours,
.dots,
.minutes {
  display: flex;
  justify-content: center;
  align-items: center;
  font-weight: 600;
  padding: 0 10px;
  line-height: 125px;
}

.hours,
.minutes {
  font-size: 6.5rem;
  width: 125px;
}
.dots {
  font-size: 5em;
  color: #929292;
}

.hours {
  background: -webkit-linear-gradient(90deg, #634dff, #5fd4ff);
  -webkit-text-fill-color: transparent;
  -webkit-background-clip: text;
}

.minutes {
  background: -webkit-linear-gradient(90deg, #ff5e9a, #ffb960);
  -webkit-text-fill-color: transparent;
  -webkit-background-clip: text;
}

.right-side {
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  margin-left: 10px;
}

.period,
.seconds {
  font-size: 1.2em;
  font-weight: 500;
}

.period {
  transform: translateY(-20px);
  background: -webkit-linear-gradient(90deg, #f7b63f, #faf879);
  -webkit-text-fill-color: transparent;
  -webkit-background-clip: text;
}
.seconds {
  transform: translateY(16px);
  background: -webkit-linear-gradient(90deg, #24ff6d, #2f93f1);
  -webkit-text-fill-color: transparent;
  -webkit-background-clip: text;
}

.calender {
  display: flex;
  justify-self: center;
  align-items: center;
  font-size: 1.3em;
  font-weight: 500;
  margin-bottom: 5px;
  background: -webkit-linear-gradient(90deg, #ae4af6, #ff98d1);
  -webkit-text-fill-color: transparent;
  -webkit-background-clip: text;
}
.day-name,
.day-number,
.year {
  margin-left: 8px;
}

.dot-menu-btn {
  position: absolute;
  top: 0;
  right: 0;
  margin: 10px;
  color: #efefef;
  font-size: 1.5em;
  cursor: pointer;
}

.dot-menu {
  z-index: 999;
  position: absolute;
  top: 7px;
  right: 5px;
  list-style: none;
  background: #353e54;
  padding: 10px 20px;
  border-radius: 5px;
  box-shadow: 0 5px 25px rgba(0, 0, 0, 0.5);
  visibility: hidden;
  opacity: 0;
  transition: 0.3 ease;
}
.dot-menu.active {
  visibility: visible;
  opacity: 1;
}
.menu-item {
  display: flex;
  justify-content: center;
  align-items: center;
}

.clock-format-text {
  color: #efefef;
  font-size: 0.9em;
  margin-right: 20px;
}

.format-switch-btn {
  width: 35px;
  height: 15px;
  background: #485470;
  border-radius: 75px;
  box-shadow: inset 2px 2px 4px rgba(255, 255, 255, 0.1),
    inset -2px -2px 4px rgba(0, 0, 0, 0.2);
  cursor: pointer;
  display: flex;
  justify-content: center;
  align-items: center;
}

.format-switch-btn:before {
  content: "";
  position: absolute;
  width: 14px;
  height: 14px;
  background: #ff5e9a;
  border-radius: 50%;
  box-shadow: 0 5px 25px #ff5e9a;
  transform: translateX(-10px);
  transition: 0.3s ease;
  transition-property: background, transform;
}

.format-switch-btn.active:before {
  background: #0bff8d;
  box-shadow: 0 5px 25px #0bff8d;
  transform: translateX(10px);
}
</style> -->
