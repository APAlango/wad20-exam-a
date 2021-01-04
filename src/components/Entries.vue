<template>
  <div class="wrapper">
    <button @click="sortedEntries">{{ this.buttonLabel }}</button>
    <div v-for="(entry, id) in entries" :key="id">
      <div class="entry-wrapper">
        <h2>{{entry.title}}</h2>
        <small>{{entry.date | readable}}</small>
        <br>
        <img :src="entry.image">
        <p>{{entry.text}}</p>
      </div>
    </div>
  </div>
</template>

<script>
    export default {
        name: 'Entries',
        props: {
            entries: Array
        },
        buttonLabel: "Newest to Oldest",
        clickBoolean: false,
        computed: {
            sortedEntries: function () {
                let sorted = this.entries
                sorted.sort((a, b) => {
                    if (this.clickBoolean) {
                        return Date.parse(a.date) - Date.parse(b.date)
                    } else {
                        return Date.parse(b.date) - Date.parse(a.date)
                    }
                })
                this.changeClicked()
                return sorted
            },

        },
        methods: {
            changeClicked: function () {
                this.clickBoolean = !this.clickBoolean
            }
        },
        filters: {
            readable: function (someDate) {
                const theDate = new Date(someDate)
                let dayOfWeek = theDate.getDay()
                switch (dayOfWeek) {
                    case 0:
                        dayOfWeek = "Monday"
                        break
                    case 1:
                        dayOfWeek = "Tuesday"
                        break
                    case 2:
                        dayOfWeek = "Wednesday"
                        break
                    case 3:
                        dayOfWeek = "Thursday"
                        break
                    case 4:
                        dayOfWeek = "Friday"
                        break
                    case 5:
                        dayOfWeek = "Saturday"
                        break
                    case 6:
                        dayOfWeek = "Sunday"
                        break
                }
                let dayOfMonth = theDate.getDate()
                let month = theDate.getMonth()
                switch (month) {
                    case 0:
                        month = "January"
                        break
                    case 1:
                        month = "February"
                        break
                    case 2:
                        month = "March"
                        break
                    case 3:
                        month = "April"
                        break
                    case 4:
                        month = "May"
                        break
                    case 5:
                        month = "June"
                        break
                    case 6:
                        month = "July"
                        break
                    case 7:
                        month = "August"
                        break
                    case 8:
                        month = "September"
                        break
                    case 9:
                        month = "October"
                        break
                    case 10:
                        month = "November"
                        break
                    case 11:
                        month = "December"
                        break
                }
                let year = theDate.getFullYear()
                let timeParts = someDate.split(" ")[1].split(":")
                let time = ""
                if (parseInt(timeParts[0]) < 12) {
                    time = parseInt(timeParts[0]) + ":" + timeParts[1] + " AM"
                } else {
                    time = (parseInt(timeParts[0]) - 12).toString() + ":" + timeParts[1] + " PM"
                }
                return dayOfWeek + ", " + month + " " + dayOfMonth + ", " + year + " " + time
            }
      }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    * {
      text-align: center;
    }
    h3 {
        margin: 40px 0 0;
    }

    ul {
        list-style-type: none;
        padding: 0;
    }

    li {
        display: inline-block;
        margin: 0 10px;
    }

    a {
        color: #42b983;
    }
</style>
