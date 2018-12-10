<template>
  <div class="main">
    <ul>
      <li
        :class="[selectedTab === tab ? 'active': '' ,'col-3']"
        v-for="tab in tabs"
        :key="tab"
        @click="displayPage(tab)"
      >{{ tab }}</li>
    </ul>

    <div class="scroll">
      <transition name="slide-fade">
        <div v-if="selectedTab === 'All Due'">
          <div v-for="card in cards" :key="card.Id" class="all-due">
            <div class="emp-details">
              <div class="employee-image row">
                <div class="col-2">
                  <img v-bind:src="image" :style="styleImage">
                </div>
                <div class="col-5">
                  <p style="margin-bottom:0px">{{ card.name }}</p>
                  <span>{{card.raised}}</span>
                </div>
                <div class="col-5">
                  <span>Auto Approval : 15 Jul</span>
                  <span>{{card.Id}}</span>
                </div>
              </div>
              <span>{{card.type}}</span>
              <br>
              <span>Duration : 12 Days | From : 10 Dec | To: 21 Dec</span>
              <br>
              <span>{{card.requestType}}</span>

              <div class="row">
                <!-- Button trigger modal -->
                <button
                  type="button"
                  class="btn btn-primary col-6"
                  data-toggle="modal"
                  data-target="#exampleModal"
                  @click="toggle()"
                >Reject</button>
                <button
                  type="button"
                  class="btn btn-primary col-6"
                  data-toggle="modal"
                  data-target="approve"
                  @click="toggleApprove()"
                >Accept</button>



                <!-- Modal Approve -->
                <div
                  v-if="showModelA"
                  :class="showModelA ? 'show' : ''"
                  class="modal fade"
                  id="exampleModal"
                  tabindex="-1"
                  role="dialog"
                  aria-labelledby="exampleModalLabel"
                  aria-hidden="true"
                >
                  <div class="modal-dialog" role="document">
                    <div class="modal-content">
                      <div class="modal-header">
                        <h5 class="modal-title" id="exampleModalLabel">Approve Request</h5>
                      </div>
                      <div class="modal-body">
                        <input type="text">
                      </div>
                      <div class="modal-footer">
                        <button
                          type="button"
                          class="btn btn-secondary"
                          @click="toggleApprove()"
                          data-dismiss="modal"
                        >Cancel</button>
                        <button
                          type="button"
                          class="btn btn-primary"
                          @click="toggleApprove()"
                        >Confirm Approval</button>
                      </div>
                    </div>
                  </div>
                </div>

                <!-- Modal Reject -->
                <div
                  v-if="showModel"
                  :class="showModel ? 'show' : ''"
                  class="modal fade"
                  id="exampleModal"
                  tabindex="-1"
                  role="dialog"
                  aria-labelledby="exampleModalLabel"
                  aria-hidden="true"
                >
                  <div class="modal-dialog" role="document">
                    <div class="modal-content">
                      <div class="modal-header">
                        <h5 class="modal-title" id="exampleModalLabel">Reject Request</h5>
                      </div>
                      <div class="modal-body">
                        <input type="text">
                      </div>
                      <div class="modal-footer">
                        <button
                          type="button"
                          class="btn btn-secondary"
                          @click="toggle()"
                          data-dismiss="modal"
                        >Cancel</button>
                        <button
                          type="button"
                          class="btn btn-primary"
                          @click="toggle()"
                        >Confirm Rejection</button>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </div>

            
            <br>
          </div>
        </div>
      </transition>
      <!-- Pending Page -->
      <transition name="slide-fade">
        <div v-if="selectedTab === 'Pending'">
          <div v-for="card in Pending_cards" :key="card.Id" class="pending">
            <div class="emp-details">
              <div class="employee-image row">
                <div class="col-2">
                  <img v-bind:src="image" :style="styleImage">
                </div>
                <div class="col-5">
                  <p style="margin-bottom:0px">{{ card.name }}</p>
                  <span>{{card.raised}}</span>
                </div>
                <div class="col-5">
                  <span>Auto Approval : 15 Jul</span>
                  <span>{{card.Id}}</span>
                </div>
              </div>
              <span>{{card.type}}</span>
              <br>
              <span>Duration : 12 Days | From : 10 Dec | To: 21 Dec</span>
              <br>
              <span>{{card.requestType}}</span>

              <div class="row">
                <!-- Button trigger modal -->
                <button
                  type="button"
                  class="btn btn-primary col-6"
                  data-toggle="modal"
                  data-target="#exampleModal"
                  @click="toggle()"
                >Reject</button>
                <button
                  type="button"
                  class="btn btn-primary col-6"
                  data-toggle="modal"
                  data-target="#exampleModal"
                  @click="toggle()"
                >Accept</button>

                <!-- Modal -->
                <div
                  v-if="showModel"
                  :class="showModel ? 'show' : ''"
                  class="modal fade"
                  id="exampleModal"
                  tabindex="-1"
                  role="dialog"
                  aria-labelledby="exampleModalLabel"
                  aria-hidden="true"
                >
                  <div class="modal-dialog" role="document">
                    <div class="modal-content">
                      <div class="modal-header">
                        <h5 class="modal-title" id="exampleModalLabel">Reject Request</h5>
                      </div>
                      <div class="modal-body">
                        <input type="text">
                      </div>
                      <div class="modal-footer">
                        <button
                          type="button"
                          class="btn btn-secondary"
                          @click="toggle()"
                          data-dismiss="modal"
                        >Cancel</button>
                        <button
                          type="button"
                          class="btn btn-primary"
                          @click="toggle()"
                        >Confirm Rejection</button>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </div>
            <br>
          </div>
        </div>
      </transition>

      <!-- Auto Apprval -->
      <transition name="slide-fade">
        <div v-if="selectedTab === 'Auto Approval'">
          <div v-for="card in AutoApprval" :key="card.Id" class="autoapproval">
            <div class="emp-details">
              <div class="employee-image row">
                <div class="col-2">
                  <img v-bind:src="image" :style="styleImage">
                </div>
                <div class="col-5">
                  <p style="margin-bottom:0px">{{ card.name }}</p>
                  <span>{{card.raised}}</span>
                </div>
                <div class="col-5">
                  <span>Auto Approval : 15 Jul</span>
                  <span>{{card.Id}}</span>
                </div>
              </div>
              <span>{{card.type}}</span>
              <br>
              <span>Duration : 12 Days | From : 10 Dec | To: 21 Dec</span>
              <br>
              <span>{{card.requestType}}</span>

              <div class="row">
                <!-- Button trigger modal -->
                <button
                  type="button"
                  class="btn btn-primary col-6"
                  data-toggle="modal"
                  data-target="#exampleModal"
                  @click="toggle()"
                >Reject</button>
                <button
                  type="button"
                  class="btn btn-primary col-6"
                  data-toggle="modal"
                  data-target="#exampleModal"
                  @click="toggle()"
                >Accept</button>

                <!-- Modal -->
                <div
                  v-if="showModel"
                  :class="showModel ? 'show' : ''"
                  class="modal fade"
                  id="exampleModal"
                  tabindex="-1"
                  role="dialog"
                  aria-labelledby="exampleModalLabel"
                  aria-hidden="true"
                >
                  <div class="modal-dialog" role="document">
                    <div class="modal-content">
                      <div class="modal-header">
                        <h5 class="modal-title" id="exampleModalLabel">Reject Request</h5>
                      </div>
                      <div class="modal-body">
                        <input type="text">
                      </div>
                      <div class="modal-footer">
                        <button
                          type="button"
                          class="btn btn-secondary"
                          @click="toggle()"
                          data-dismiss="modal"
                        >Cancel</button>
                        <button
                          type="button"
                          class="btn btn-primary"
                          @click="toggle()"
                        >Confirm Rejection</button>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </div>
            <br>
          </div>
        </div>
      </transition>

      <!-- Completed -->
      <transition name="slide-fade">
        <div v-if="selectedTab === 'COMPLETED'">
          <div v-for="card in Completed" :key="card.Id" class="autoapproval">
            <div class="emp-details">
              <div class="employee-image row">
                <div class="col-2">
                  <img v-bind:src="image" :style="styleImage">
                </div>
                <div class="col-5">
                  <p style="margin-bottom:0px">{{ card.name }}</p>
                  <span>{{card.raised}}</span>
                </div>
                <div class="col-5">
                  <span>{{card.status}}</span>
                  <span>{{card.Id}}</span>
                </div>
              </div>
              <span>{{card.type}}</span>
              <br>
              <span>Duration : 12 Days | From : 10 Dec | To: 21 Dec</span>
              <br>
              <span>{{card.requestType}}</span>
            </div>
            <br>
          </div>
        </div>
      </transition>
    </div>
  </div>
</template>

<script>
const tabs = ["All Due", "Pending", "Auto Approval", "COMPLETED"];
export default {
  data() {
    return {
      styleImage: {
        width: "30px",
        Height: "30px",
        margin: "10px"
      },
      image: "./view.jpg",
      tabs,
      selectedTab: tabs[0],
      showModel: false,
      showModelA: false,
      Completed: [
        {
          name: "Roy Thompson",
          Id: "1011",
          raised: "10 Jul",
          requestType: "Leave Request",
          status: "Approved"
        },
        {
          name: "Tara Cunninghum",
          Id: "2012",
          raised: "5 Dec",
          requestType: "VSEC Approval",
          status: "Rejected"
        },

        {
          name: "Ruben Ray",
          Id: "1061",
          raised: "30 Nov",
          requestType: "Leave Request",
          status: "Auto Approved"
        }
      ],
      Pending_cards: [
        {
          name: "Roy Thompson",
          Id: "1011",
          raised: "10 Jul",
          requestType: "Leave Request"
        },
        {
          name: "Tara Cunninghum",
          Id: "2012",
          raised: "5 Dec",
          requestType: "VSEC Approval"
        }
      ],
      AutoApprval: [
        {
          name: "Ruben Ray",
          Id: "1061",
          raised: "30 Nov",
          requestType: "Leave Request"
        }
      ],
      cards: [
        {
          name: "Roy Thompson",
          Id: "1011",
          raised: "10 Jul",
          requestType: "Leave Request"
        },
        {
          name: "Tara Cunninghum",
          Id: "2012",
          raised: "5 Dec",
          requestType: "VSEC Approval"
        },
        {
          name: "Ruben Ray",
          Id: "1061",
          raised: "30 Nov",
          requestType: "Leave Request"
        },
        {
          name: "Ruben Ray",
          Id: "5012",
          raised: "10 Sept",
          requestType: "VSEC Approval"
        },
        {
          name: "Roy Thompson",
          Id: "1154",
          raised: "30 Nov",
          requestType: "Leave Request"
        }
      ]
    };
  },
  methods: {
    displayPage(page) {
      console.log("This is ", page, "page");
      this.selectedTab = page;
    },
    toggle() {
      this.showModel = !this.showModel;
    },
    toggleApprove() {
      this.showModelA = !this.showModelA;
    }
  }
};
</script>

<style>
.emp-details {
  margin: 5px;
  border-radius: 5px;
  background-color: white;
}
.main {
  width: 100%;
  height: 100vh;
  display: flex;
  flex-direction: column;
}
span {
  font-size: 10px;
}

.scroll {
  overflow-y: auto;
  overflow-x: hidden;
}
ul {
  padding: 0px;
  list-style-type: none;
}

li {
  padding-top: 10px;
  font-size: 10px;
  display: inline-block;
  text-align: center;
  cursor: pointer;
  color: grey;
  border-bottom: 1px solid lightgray;
}
li:hover {
  color: black;
  background-color: lightgrey;
}
.active {
  border-bottom: 2px solid black;
}

.modal.show {
  display: block;
}
.slide-fade-enter-active {
  transition: all 0.3s ease;
}
.slide-fade-leave-active {
  transition: all 0.6s cubic-bezier(1, 0.5, 0.8, 1);
}
.slide-fade-enter, .slide-fade-leave-to
/* .slide-fade-leave-active below version 2.1.8 */ {
  transform: translateX(10px);
  opacity: 0;
}
</style>
