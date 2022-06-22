<template>
  <div class="profile">
    <h1>This is an profile </h1>
    <v-card-actions>
    <v-spacer />
    <v-btn v-on:click="show_profile" color="primary">ログイン</v-btn>
    </v-card-actions>
    <img id=" image" >
  </div>
</template>


<script>
import { getStorage, ref, getBlob } from 'firebase/storage'

export default {
    methods: {
        async get_profile(){
            const storage = getStorage()
            const imageRef = ref(storage,`profile/tanimoto.jpeg`)
            await getBlob(imageRef)
            .then((blob) => {
            const blobURL = URL.createObjectURL(blob)
            return blobURL
          })
          .catch((e) => {
            console.error(e)
          })
        },
        show_profile(){
            const url = this.get_profile()
            // 要素の取得
            let img = document.getElementById('image')
            img.src = url
        }
    },
}
</script>