<template>
    <div class="room border border-secondary rounded p-2 mb-2" :class="{expanded: isExpanded}">
      <div class="top-row d-flex" @click="toggleExpand">
        <div class="room-name fw-bold pe-3">{{room.name}}</div>
        <div class="building-name text-muted">{{room.buildingName}}</div>
        <div class="expand-button ms-auto">
          {{ isExpanded ? '&#9660;' : '&#9658;' }}
        </div>
      </div>
      <template v-if="isExpanded">
        <hr/>
        <div class="details d-flex">
            <div class="room-name text-muted pe-3">Floor : {{ room.floor }}</div>
            <div
            v-if="room.current_temperature != null"
            class="current-Temperature text-muted pe-3 mx-2"
          >
            Current Temperature : {{ room.current_temperature }}
          </div>
          <div
            v-if="room.target_temperature != null"
            class="target_temperature text-muted pe-3"
          >
          Target temperature : {{ room.target_temperature }}
          </div>

          <button type="button" class="btn btn-danger me-2" @click="deleteRoom">
            Delete room
          </button>

  
        </div>
      </template>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  import {API_HOST} from '../config';
  
  export default {
    name: 'RoomsListItem',
    props: ['room'],
    data: function() {
      return {
        isExpanded: false
      }
    }, 
    methods: {
      toggleExpand() {
        this.isExpanded = !this.isExpanded;
      },
      async deleteRoom() {
        let response = await axios.delete(
          `${API_HOST}/api/rooms/${this.room.id}`
        );
        this.$emit("room-deleted", this.room.id);
      },
  
    }
  }
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
        top: -3px;
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
  