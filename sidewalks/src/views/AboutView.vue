<template>
  <div class="about">
    about
  </div>
</template>

<script>

/* eslint-disable */
import firebase from '@/helpers/firebase'
import { connectStorageEmulator } from '@firebase/storage';
import { doc, deleteDoc } from "firebase/firestore";



export default {
  data () {
    return {
      firestore: null,
    }
  },
  methods: {

  },
  mounted() {
    this.firestore = firebase.firestore()
  }
}

</script>
