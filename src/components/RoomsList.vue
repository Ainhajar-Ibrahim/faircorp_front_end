<template>
    <div class="rooms-list pt-3">
      <rooms-list-item 
        v-for="room in rooms"
        :room="room"
        :key="room.id"  
        @room-deleted="deleteRoom"
      >
      </rooms-list-item>
      <room-create
        @room-created="createRoom"
      >
      </room-create>
  
    </div>
  </template>
  
  
  <script>
  import axios from 'axios';
  import {API_HOST} from '../config';
  import RoomsListItem from './RoomsListItem';
  import RoomCreate from './RoomCreate.vue';
  
  export default {
    components: {
      RoomsListItem,
      RoomCreate
    },
    name: 'RoomsList',
    data: function() {
      return {
        /* Initialize rooms with an empty array, while waiting for actual data to be retrieved from the API */
        rooms: []
      }
    },
    created: async function() {
      let response = await axios.get(`${API_HOST}/api/rooms`);
      let rooms = response.data;
      this.rooms = rooms;
    },
    methods: {
      deleteRoom(roomId) {
        let index = this.rooms.findIndex(room => room.id === roomId);
        if (index > -1) {
      this.rooms.splice(index, 1);
        }
      },
  
      createRoom(newRoom) {
      this.rooms.push(newRoom);
      }
  
  
    }
  }
  </script>