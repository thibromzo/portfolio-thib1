<script setup>
    defineProps ({
      modalConfig : Object
    });

    const emit = defineEmits(["closeClicked"]);

    function onClickClose() {
        emit("closeClicked")
    };
</script>

<template>
    <div @click="onClickClose()" :style="{ display: modalConfig.display }" class="modal">
      <div class="modal-content col-flex-wrap-center">
        <h2>{{ modalConfig.content.title }}</h2>
        <ul>
          <template v-for="(item, key) in modalConfig.content">
            <li v-if="item.hasOwnProperty('isLink')">
              <span class="line-title">{{ key }}</span> : <a :href="item.link" target="_blank">{{ item.link }}</a>
            </li>
            <li v-else>
              <span class="line-title">{{ key }}</span> : {{ item }}
            </li>
          </template>
        </ul>
        <button title="Fermer" class="close" @click="onClickClose()">Fermer</button>
      </div>
    </div>
</template>

<style scoped>
  h2 {
    margin-left: auto;
    margin-right: auto;
    margin-top: 0.5rem;
    margin-bottom: 1rem;
  }

  button {
    margin-top: 1rem;
    margin-bottom: 1rem;
  }

  .line-title {
    font-weight: bold;
  }

.modal {
  position: fixed;
  padding-top: 5%;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  overflow: auto;
  background-color: rgba(0,0,0,0.4);
}

.modal-content {
  align-items: center;
  margin: auto;
  padding-left: 1rem;
  padding-right: 1rem;
  width: 30%;
  background-color: #fefefe;
  border: solid 1px black;
  border-radius: 15% 5%;
}

.close {
  justify-self: flex-end;
  color: black;
}

.close:hover, .close:focus {
  color: blue;
  cursor: pointer;
}
</style>