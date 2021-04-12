<template>
  <div class="container">
      <div class="post_container">
          <div class="post" v-for="data in data" :key="data.id">
              <div class="row">
                <p>{{data.created_at}}</p>
                <p>{{data.user.name}}</p>
              </div>
              <p>{{data.text}}</p>
          </div>
      </div>
  </div>
</template>

<script>
export default {
    props:['amountPosts', 'url', 'interval'],
data(){
    return{
       data: ""
    };
},
methods:{
    async getData(){
        const rez = await fetch(this.url)
        this.data = await rez.json()
        this.data.splice(this.amountPosts, (this.data.length - this.amountPosts))
        for(let cur of this.data){
            cur.created_at = this.changeDate(cur.created_at);
        }
    },
    changeDate(date){
        const event = new Date(date);
        return  event.toLocaleString()
    }
},
async mounted(){
    this.getData();
    const timerId = setInterval(this.getData, this.interval);
},
destroyed(){
    clearInterval(timerId)
}
}
</script>

<style scoped>
.container{
    width: 100%;
    min-height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
}
.post_container{
    display: flex;
    flex-direction: column;
}
.row{
    display: flex;
    justify-content: space-between;
}
</style>