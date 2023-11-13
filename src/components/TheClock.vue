<script>

export default {
    data() {
        return {
            time: "",
            date: ""
        }
    },
    methods: {
        TheClock() {
            console.log("theClock()");
  
    /*const full_date = new Date().toLocaleDateString(); //Date String
    const full_time = new Date().toLocaleTimeString(); // Time String*/
    //Annat sätt att göra allt nedanför
  
    let date = new Date();
    let day = date.getDate();
    let mo = date.getMonth() + 1;
    let year = date.getFullYear();
    let hh = date.getHours();
    let mm = date.getMinutes();
    let ss = date.getSeconds();
  
    /*
    Sätter 0 framför ifall värdet är under 10
    https://flexiple.com/javascript/javascript-clock/
    */
    hh = (hh < 10) ? "0" + hh : hh;
    mm = (mm < 10) ? "0" + mm : mm;
    ss = (ss < 10) ? "0" + ss : ss;
    day = (day < 10) ? "0" + day : day;
    mo = (mo < 10) ? "0" + mo : mo; //operand,  (condition ? if true : if false);
  
    this.time = `${hh}:${mm}:${ss}`;
    this.date = `${day}.${mo}.${year}`;

        }
    },
    mounted() {
        this.TheClock();
        setInterval(this.TheClock, 1000);
    }
}

</script>

<template>

    <div id="date" v-html="date" ></div>
    <div id="clock" v-html="time" ></div>

</template>