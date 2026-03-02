<script>
export default {
  name: "User",
  data(){
    return{
      userName:"Sultan",
      isEditing:false,
      tempName:"",
    }
  },
  methods:{
    startEdit(){
      this.tempName= this.userName;
      this.isEditing=true
    },
    saveEdit(){
      this.userName= this.tempName;
      this.isEditing=false

    }
  }
}
</script>

<template>
  <div class="rounded-lg border  md:border-green-800 bg-emerald-800/20 flex p-4 gap-3 mb-4"   >
    <div class="w-12 h-12  rounded-full bg-emerald-600 flex items-center justify-center text-emerald-100 ">
      <svg xmlns="http://www.w3.org/2000/svg"
           width="24"
           height="24"
           viewBox="0 0 24 24"
           fill="none"
           stroke="currentColor"
           stroke-width="2"
           stroke-linecap="round"
           stroke-linejoin="round"
           class="">
        <path d="M19 21v-2a4 4 0 0 0-4-4H9a4 4 0 0 0-4 4v2"/>
        <circle cx="12" cy="7" r="4"/></svg>
    </div>


    <div class="" >
    <div class="flex">
      <h1 class="font-bold text-base text-emerald-100" v-if="!isEditing" >{{userName}}</h1>
      <input
          v-if="isEditing"
          v-model="tempName"
          @keyup.exact.enter="saveEdit"
          class="border px-2 py-1 rounded"
      />
      <button class=" md:border-green-800 hover:bg-emerald-500/40" v-if="isEditing" @click="saveEdit">
        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="text-emerald-100">
          <path d="M20 6 9 17l-5-5"/></svg>
      </button>
      <button class="h-6 w-6 flex items-center justify-center hover:bg-emerald-500/40"
              v-if="!isEditing" @click="startEdit" >
        <svg xmlns="http://www.w3.org/2000/svg"
             width="24"
             height="24"
             viewBox="0 0 24 24"
             fill="none"
             stroke="currentColor"
             stroke-width="3"
             stroke-linecap="round"
             stroke-linejoin="round"
             class="w-3 h-3 text-emerald-600">
          <path d="M21.174 6.812a1 1 0 0 0-3.986-3.987L3.842 16.174a2 2 0 0 0-.5.83l-1.321 4.352a.5.5 0 0 0 .623.622l4.353-1.32a2 2 0 0 0 .83-.497z"/></svg>
      </button>
    </div>


    <h4 class="text-xs text-emerald-400/60">Notepad user</h4>
    </div>
  </div>

</template>


<style scoped>

</style>