<template>
    <div class="card">
      <div class="card-header">
        <h2 class="mb-0">
          <button
            class="btn btn-link btn-block text-left d-flex"
            type="button"
            @click="toggleExpand"
          >
            <div class="mr-2">Create New Room</div>
            <div class="expand-button ml-auto ">
              {{ isExpanded ? "&#9660;" : "&#9658;" }}
            </div>
          </button>
        </h2>
      </div>
  
      <template class="collapse show" v-if="isExpanded">
        <form class="p-4">
          <div class="form-group">
            <label for="room_name">Room Name: </label>
            <input
              v-model="room_name"
              type="text"
              class="form-control"
              name="room_name"
              id="room_name"
              placeholder="room"
            />
          </div>
          <div class="form-group">
            <label for="room_building">Building name: </label>
            <select
              class="form-control"
              v-model="room_building"
              id="room_building"
              name="room_building"
            >
              <option v-for="building in buildings" v-bind:value="building">
                {{ building.name }}
              </option>
            </select>
          </div>
          <div class="form-group">
            <label for="room_floor">Room Floor: </label>
            <input
              v-model="room_floor"
              type="text"
              class="form-control"
              name="room_floor"
              id="room_floor"
            />
          </div>
          <div class="form-group">
            <label for="current_temperature">current temperature: </label>
            <input
              v-model="current_temperature"
              type="text"
              class="form-control"
              name="current_temperature"
              id="current_temperature"
            />
          </div>
          <div class="form-group">
            <label for="target_temperature">Target temperature: </label>
            <input
              v-model="target_temperature"
              type="text"
              class="form-control"
              name="target_temperature"
              id="target_temperature"
            />
          </div>

          <hr/>
          <button type="button" class="btn btn-primary" @click="createRoom">
            Create Room
          </button>
        </form>
      </template>
    </div>
  </template>
  
  
  <script>
  import axios from "axios";
  import { API_HOST } from "../config";
  
  export default {
    name: "RoomCreate",
    data: function () {
      return {
        isExpanded: false,
        room_name: "",
        room_building: "",
        room_floor:"",
        current_temperature:"",
        terget_temperature:"",
        buildings: [],
      };
    },
    created: async function () {
      let response = await axios.get(`${API_HOST}/api/buildings`);
      let buildings = response.data;
      this.buildings = buildings;
      this.room_building = buildings[0];
    },
    methods: {
      toggleExpand() {
        this.isExpanded = !this.isExpanded;
      },
      async createRoom() {
        let newRoom = {
          name: this.room_name,
          buildingId: this.room_building.id,
          floor: this.room_floor,
          current_temperature: this.current_temperature,
          target_temperature:this.target_temperature,
        };
        let headers = {
          "Content-Type": "application/json",
        };
        let response = await axios.post(`${API_HOST}/api/rooms`, newRoom, {
          headers,
        });
        this.$emit("room-created", response.data);
      },
    },
  };
  </script>
  
  <style lang="scss" scoped>
  .open-status {
    .icon {
      position: relative;
    }
  
    &.open {
      color: #198754;
      .icon {
        font-size: 12px;
        top: -2px;
      }
    }
  
    &.closed {
      color: #dc3545;
    }
  }
  
  .room {
    .top-row {
      cursor: pointer;
    }
  }
  </style>