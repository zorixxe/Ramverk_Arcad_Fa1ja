<script>

import ical from 'ical';

export default {
    data() {
        return {
            link: "https://corsproxy.io/?https://famnen.arcada.fi/arbs/public/ical/timetable.php?hash=e8232f53ddb05042d89eab6c3e571ad4",
            courses: [] //tanken var först att mata från courses arrayn till today_arrayn men i slutändan behövdes bara en array
        };
    },
    methods: {
        async parseIcal() {
            const response = await fetch(this.link);
            const ics = await response.text();
            const data = await ical.parseICS(ics);
            const today = new Date()
            for (let k in data) {
                if (data.hasOwnProperty(k)) {
                    var ev = data[k];
                    if (data[k].type == "VEVENT") {
                        const eventStartDate = new Date(ev.start)
                        if (eventStartDate.getDate() === today.getDate() && ev.location) { // lade till && ev.location så visar den inte lektioner utan rumsbokning (annars visar den lektion i december utan rumsbokning)
                            this.courses.push({
                                course: ev.summary,
                                startdate: ev.start, //eller eventStartDate går med båda.
                                endtime: ev.end.toLocaleTimeString("fi-FI"),
                                room: ev.location,
                            });
                        }
                    }
                }
            }
            console.log(this.courses);
        },
        formatTime(startDate) {
            const date = new Date(startDate);
            const hours = date.getHours().toString().padStart(2, "0");
            const minutes = date.getMinutes().toString().padStart(2, "0");
            return `${hours}:${minutes}`;
        },
        formatEndTime(endTime) {
            const parts = endTime.split(".");
            endTime = parts[0] + ":" + parts[1];
            return endTime;
        },
    },
    mounted() {
        this.parseIcal();
    },
};
</script>

<template>
    <div class="classes">
        <div class = "classText" v-for="(course, index) in courses" :key="index">
            <h2 class="course">{{ course.course }}</h2>

            <div class="timeBar">
                <div class="timeBox">
                    <p class="time">
                        {{ formatTime(course.startdate) }} -
                        {{ formatEndTime(course.endtime) }}
                    </p>
                </div>
                <div class="roomBox">
                    <p class="room">{{ course.room }}</p>
                </div>
            </div>
        </div>
    </div>
</template>
