<template>
  <main class="daycounter-app">
    <input class="daycounter-app__input" @input="calculateDate($event)" type="date">
    <h1 class="daycounter-app__header">Количество дней вашей жизни:</h1>
    <div class="daycounter-app__result-section result-section">
      <div class="result-section__result-wrapper result-wrapper">
        <div class="result_wrapper__result">{{totalLifeDays}}</div>
      </div>
    </div>
  </main>
</template>

<script>
export default {
  data(){
    return {
      birthDate: "",
      totalLifeDays:0
    }
  },
  methods: {
    calculateDate(event){
      this.birthDate = event.target.value;
      let daysBeforeBirth, daysInBirthYearBeforeBirthMonth;
      
      // Array birthYearMonthDayArray represents birth year, birth month, birth day. 
      // The array data is accessible through the corresponding index [0], [1], [2].
      let birthYearMonthDayArray = this.birthDate.split("-");
      switch (Number(birthYearMonthDayArray[1])){
        case 1: daysInBirthYearBeforeBirthMonth = 0; break;
        case 2: daysInBirthYearBeforeBirthMonth = 31; break;
        case 3: daysInBirthYearBeforeBirthMonth = 59; break;
        case 4: daysInBirthYearBeforeBirthMonth = 90; break;
        case 5: daysInBirthYearBeforeBirthMonth = 120; break;
        case 6: daysInBirthYearBeforeBirthMonth = 151; break;
        case 7: daysInBirthYearBeforeBirthMonth = 181; break;
        case 8: daysInBirthYearBeforeBirthMonth = 212; break;
        case 9: daysInBirthYearBeforeBirthMonth = 243; break;
        case 10: daysInBirthYearBeforeBirthMonth = 273; break;
        case 11: daysInBirthYearBeforeBirthMonth = 304; break;
        case 12: daysInBirthYearBeforeBirthMonth = 334; break;
      }

      // If the year of birth is a leap year and the month of birth is after February, then the extra day is counted.
      if (Number(birthYearMonthDayArray[0])%4===0 && Number(birthYearMonthDayArray[1])>=3){
        daysInBirthYearBeforeBirthMonth++;
      }

      // Substracting the days before birth from the current date and recieve total days of life.
      // note: Date.now() method returns the number of milliseconds elapsed since January 1, 1970.
      daysBeforeBirth = daysInBirthYearBeforeBirthMonth + Number(birthYearMonthDayArray[2])-1 + (Number(birthYearMonthDayArray[0])*365 + Math.floor(Number(birthYearMonthDayArray[0])/4));
      this.totalLifeDays = (1970*365 + Math.floor(1970/4)) + Math.floor(Date.now()/(1000*60*60*24)) - daysBeforeBirth;
    }
  }
}
</script>
<style>
* {
  font-family: serif;
  margin:0;
  padding: 0;
  box-sizing: border-box;
  text-shadow: 1px 1px 1px black;
}
.daycounter-app {
  width: 100vw;
  height: 100vh;
  background: linear-gradient(rgb(29, 47, 82), rgb(72, 64, 100) 43% 69%, rgb(38, 71, 99));
  display: flex;
  align-items: center;
  flex-direction: column;
  justify-content: center;
}
.daycounter-app > *{
  margin-top: 1.3rem;
}
.daycounter-app__input{
  width:240px;
  text-shadow: none;
  font-size: 0.9rem;
  border: 2px solid black;
  border-radius: 5px;
}
.daycounter-app__input::before{
  content: "Дата рождения:";
  font-weight: bold;
  border-radius: 2px;
  margin: 2px;
  padding:3px;
  background: rgb(173, 172, 172);
}
.daycounter-app__header{
  padding: 0 15px;
  color:rgb(255, 255, 56);
  text-align: center;
  font-size:1.6rem;
}
.daycounter-app__result-section {
  width:11vmax;
  height:11vmax;
  display:flex;
  align-items: center;
  justify-content: center;
}
.result-section__result-wrapper {
  width:100%;
  height:100%;
  border-radius: 50%;
  border: 3px solid rgb(255, 255, 56);
  background:rgb(126, 126, 120);
  color: rgb(255, 255, 56);
  display:flex;
  align-items: center;
  justify-content: center;
}
.result_wrapper__result {
  max-width: 85%;
  font-size: 26px;
}
</style>
