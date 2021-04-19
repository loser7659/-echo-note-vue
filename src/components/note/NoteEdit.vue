<template>
  <div>
    <mavon-editor
      v-model="note.contentMd"
      @save="saveNote"
    >

    </mavon-editor>
  </div>
</template>

<script>
export default {
  name: "NoteEdit",
  data(){
    return{
      note:{
        contentMd:''
      }
    }
  },
  mounted() {
    if (this.$route.query.noteId){
      this.loadNote(this.$route.query.noteId)
    }
  },
  methods:{
    loadNote(id){
      const _this = this
      this.axios.get('note/'+id.toString())
      .then(function (response){
        if(response.data.status===200){
          _this.note = response.data.object
        }
        console.log(response.data.object)
      })
    },
    saveNote(value,render){
      const _this = this
      const url = '/update/content/note/' + this.note.id;
      this.note.contentMd =value
      this.note.contentHtml = render
      this.axios.post(url,this.note)
      .then(function (response){
        if(response.data.status === 200){
          _this.$message({
            type:'success',
            message:'保存成功'
          })
        }
      })
    }
  }
}
</script>

<style scoped>

</style>
