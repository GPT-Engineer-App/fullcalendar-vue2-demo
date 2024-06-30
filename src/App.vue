<template>
  <div id="app">
    <FullCalendar :options="calendarOptions" />
  </div>
</template>

<script>
import FullCalendar from '@fullcalendar/vue';
import dayGridPlugin from '@fullcalendar/daygrid';
import interactionPlugin from '@fullcalendar/interaction';

export default {
  name: 'App',
  components: {
    FullCalendar,
  },
  data() {
    return {
      calendarOptions: {
        plugins: [dayGridPlugin, interactionPlugin],
        initialView: 'dayGridMonth',
        editable: true,
        selectable: true,
        events: [
          { title: 'Event 1', date: '2023-10-01' },
          { title: 'Event 2', date: '2023-10-02' },
        ],
        dateClick: this.handleDateClick,
        eventClick: this.handleEventClick,
      },
    };
  },
  methods: {
    handleDateClick(info) {
      const title = prompt('Enter event title:');
      if (title) {
        this.calendarOptions.events.push({
          title,
          start: info.dateStr,
        });
      }
    },
    handleEventClick(info) {
      if (confirm('Do you want to delete this event?')) {
        this.calendarOptions.events = this.calendarOptions.events.filter(
          event => event !== info.event
        );
      }
    },
  },
};
</script>

<style>
@import '@fullcalendar/common/main.css';
@import '@fullcalendar/daygrid/main.css';

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>