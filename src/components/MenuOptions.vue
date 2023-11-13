<script>
export default {
    data() {
        return {
            menu: "",
            veg: ""
        }
    },
    methods: {
        async fetchMenu() {
      fetch('https://corsproxy.io/?https://www.compass-group.fi/menuapi/feed/json?costNumber=3003&language=en', {
        method: "GET",
      })
        .then((response) => {
          response.json().then((data) => {
            this.menu = data.MenusForDays[0].SetMenus[1].Components;
            this.veg = data.MenusForDays[0].SetMenus[0].Components;
          });
        })
        .catch((err) => {
          console.error(err);
        });
    
        }
    },
    mounted() {
        this.fetchMenu();
    }
}
</script>

<template>
    <div class="classes">
        <div class="MenuOptions">
            <p class="menuText" v-html="menu" ></p>
            <p class="menuText" v-html="veg" ></p>
        </div>
    </div>
</template>