<template>
  <div class="wrapper">
    <!-- challengers-modal -->
    <div id="challenger-calendar-modal" class="custom-modal m-auto">
      <div class="modal-center">
        <div class="modal-outer-box">
          <div class="modal-inner-box">
            <div class="modal-header">
              <div class="btn-modal-close ml-auto" @click="display = !display">
                <svg
                  width="36"
                  height="36"
                  viewBox="0 0 36 36"
                  xmlns="http://www.w3.org/2000/svg"
                >
                  <path
                    d="M30.7336 5.26685C23.7103 -1.75497 12.2885 -1.75497 5.2652 5.26685C-1.75507 12.2887 -1.75507 23.7135 5.2652 30.7353C8.77685 34.2455 13.3885 35.9997 18.0002 35.9997C22.6119 35.9997 27.222 34.2454 30.7336 30.7353C37.7555 23.7135 37.7555 12.2887 30.7336 5.26685ZM25.4271 23.3068C26.0139 23.8936 26.0139 24.842 25.4271 25.4288C25.1345 25.7214 24.7503 25.8685 24.3661 25.8685C23.982 25.8685 23.5977 25.7214 23.3051 25.4288L18.0001 20.1223L12.6966 25.4272C12.4025 25.7199 12.0183 25.867 11.6356 25.867C11.2515 25.867 10.8672 25.7199 10.5746 25.4272C9.98785 24.8405 9.98785 23.8905 10.5746 23.3053L15.8781 18.0003L10.5731 12.6953C9.98637 12.1086 9.98637 11.1586 10.5731 10.5734C11.1584 9.98661 12.1083 9.98661 12.6951 10.5734L18.0001 15.8783L23.305 10.5734C23.8918 9.98661 24.8402 9.98661 25.427 10.5734C26.0137 11.1586 26.0137 12.1086 25.427 12.6953L20.122 18.0003L25.4271 23.3068Z"
                  />
                </svg>
              </div>
            </div>
            <div class="modal-body px-5" v-if="display === true">
              <div class="form-container mx-auto">
                <p class="challengers-modal-title">Microsoft - DFC 2022</p>
                <p class="challengers-modal-desc">
                  <span class="start-date">Start Date on Oct 29, 2022</span>
                  <span class="start-date">-</span>
                  <span class="end-date">End Date on Nov 27, 2022</span>
                </p>
                <p class="start-date">
                  Today is: {{ currentMonthName }} - {{ currentYear }}
                </p>
              </div>
              <div
                class="challenger-calendar-box flex items-end justify-between"
              >
                <!-- svg area  -->
                <Svgs />
                <div class="calendar-outer-box">
                  <div
                    class="calendar-header flex items-center justify-between"
                  >
                    <button
                      class="btn-prev-month flex items-center active"
                      @click="prev"
                    >
                      <svg
                        class="icon-prev"
                        width="19"
                        height="16"
                        viewBox="0 0 19 16"
                        xmlns="http://www.w3.org/2000/svg"
                      >
                        <path
                          d="M18 7C18.5523 7 19 7.44772 19 8C19 8.55228 18.5523 9 18 9L18 7ZM0.292892 8.70711C-0.0976315 8.31658 -0.0976314 7.68342 0.292893 7.29289L6.65686 0.928931C7.04738 0.538407 7.68054 0.538407 8.07107 0.928931C8.46159 1.31946 8.46159 1.95262 8.07107 2.34314L2.41421 8L8.07107 13.6569C8.46159 14.0474 8.46159 14.6805 8.07107 15.0711C7.68054 15.4616 7.04738 15.4616 6.65685 15.0711L0.292892 8.70711ZM18 9L1 9L1 7L18 7L18 9Z"
                        />
                      </svg>
                      Previous
                    </button>
                    <button
                      class="btn-next-month flex items-center active"
                      @click="next"
                    >
                      Next
                      <svg
                        class="icon-next"
                        width="19"
                        height="16"
                        viewBox="0 0 19 16"
                        xmlns="http://www.w3.org/2000/svg"
                      >
                        <path
                          d="M1 7C0.447715 7 -4.82822e-08 7.44772 0 8C4.82822e-08 8.55228 0.447715 9 1 9L1 7ZM18.7071 8.70711C19.0976 8.31658 19.0976 7.68342 18.7071 7.29289L12.3431 0.928931C11.9526 0.538407 11.3195 0.538407 10.9289 0.928931C10.5384 1.31946 10.5384 1.95262 10.9289 2.34314L16.5858 8L10.9289 13.6569C10.5384 14.0474 10.5384 14.6805 10.9289 15.0711C11.3195 15.4616 11.9526 15.4616 12.3431 15.0711L18.7071 8.70711ZM1 9L18 9L18 7L1 7L1 9Z"
                        />
                      </svg>
                    </button>
                  </div>
                  <div class="calendar-body">
                    <div class="calendar-thead">
                      <div class="calendar-tr">
                        <div
                          class="calendar-th"
                          v-for="(day, index) in days"
                          :key="index"
                        >
                          {{ day }}
                        </div>
                      </div>
                    </div>
                    <div class="calendar-tbody">
                      <div class="calendar-tr">
                        <div
                          class="calendar-td flex not-selected-month"
                          v-for="day in firstDay"
                          :key="day.id"
                        >
                          <p></p>
                        </div>
                        <div
                          class="calendar-td flex flex-col not-selected-month"
                          v-for="date in lastDateOfMonth"
                          :key="date"
                          :class="todayDate(date)"
                        >
                          <p class="date">
                            {{ date }}
                          </p>
                        </div>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
              <!-- point area -->
              <point />
              <!-- profile area -->
              <profile />
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Svgs from "./components/Svg.vue";
import point from "./components/Point.vue";
import profile from "./components/Profile.vue";
export default {
  components: {
    Svgs,
    point,
    profile,
  },
  data() {
    return {
      days: ["Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat"],
      currentMonthInNumber: new Date().getMonth(),
      currentYear: new Date().getFullYear(),
      isActive: true,
      display: true,
    };
  },
  computed: {
    currentMonthName() {
      return new Date(
        this.currentYear,
        this.currentMonthInNumber
      ).toLocaleString("default", { month: "long" });
    },
    lastDateOfMonth() {
      return new Date(
        this.currentYear,
        this.currentMonthInNumber + 1,
        0
      ).getDate();
    },
    firstDay() {
      return new Date(this.currentYear, this.currentMonthInNumber, 1).getDay();
    },
  },
  methods: {
    next() {
      if (this.currentMonthInNumber === 11) {
        this.currentYear++;
        this.currentMonthInNumber = 0;
      } else {
        this.currentMonthInNumber++;
      }
    },
    prev() {
      if (this.currentMonthInNumber === 0) {
        this.currentYear--;
        this.currentMonthInNumber = 11;
      } else {
        this.currentMonthInNumber--;
      }
    },
    todayDate(date) {
      let calendarDate = new Date(
        this.currentYear,
        this.currentMonthInNumber,
        date
      ).toDateString();
      let toDay = new Date().toDateString();

      return calendarDate === toDay ? "activee" : "";
    },
  },
};
</script>

<style>
@import "./assets/css/main.css";
.activee {
  background-color: #cba8e6;
}
</style>
