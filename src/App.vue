

<template>
  <el-menu class="el-menu-demo" mode="horizontal">
    <el-menu-item index="1">
      <h1>TODO-LIST</h1>
    </el-menu-item>

  </el-menu>
  <el-row :gutter="20" style="margin-top:8px;text-align: -webkit-center;">

    <el-col :span="2">

    </el-col>
    <el-col :span="18">
      <el-input v-model="content" :placeholder="placeholder" maxlength="50" show-word-limit @keyup.enter="addList" />


    </el-col>

    <el-col :span="2" style="position: relative; top:50%;transform: translateY(0%);">


      <el-button ref="sendbtn" :type="color" @click="addList" :round="isround" :circle="iscircle" :loading="isloading">
        <el-icon>
          <Edit />
        </el-icon>
      </el-button>

    </el-col>







  </el-row>

  <el-row gutter="10" style="margin-top:14px;">

    <el-col :span="8" :xs="24" :md="6" 
      v-for="list in todolist"
      :key="list.id"  
    >
    <el-card class="box-card" shadow="hover">
        <el-row gutter="10">
          <el-col :span="2">
            <div style="position: relative; top:50%;transform: translateY(-50%); ">
              <el-checkbox v-model="list.completed" size="large" />
            </div>
          </el-col>
          <el-col :span="18">
            <div style="position: relative; top:50%;transform: translateY(-50%);">
              {{list.content}}
            </div>
          </el-col>
          <el-col :span="4">
            <div style="position: relative; top:50%;transform: translateY(-50%);text-align: -webkit-center;">
              <el-button type="danger" circle>
                <el-icon>
                  <Delete />
                </el-icon>
              </el-button>
            </div>
          </el-col>
        </el-row>
      </el-card>
    </el-col>


    <!-- <el-col :span="8" :xs="24" :md="6">
      <el-card class="box-card" shadow="hover">
        <el-row gutter="10">
          <el-col :span="2">
            <div style="position: relative; top:50%;transform: translateY(-50%); ">
              <el-checkbox v-model="ischecked" size="large" />
            </div>
          </el-col>
          <el-col :span="18">
            <div style="position: relative; top:50%;transform: translateY(-50%);">
              content
            </div>
          </el-col>
          <el-col :span="4">
            <div style="position: relative; top:50%;transform: translateY(-50%);text-align: -webkit-center;">
              <el-button type="danger" circle>
                <el-icon>
                  <Delete />
                </el-icon>
              </el-button>
            </div>
          </el-col>
        </el-row>
      </el-card>
    </el-col> -->

    
    








  </el-row>



</template>


<script >
let id=1;
export default {
  data() {
    return {
      placeholder:"Plase Input Something",
      content: "",
      color: "success",
      isround: false,
      iscircle: true,
      isloading: false,
      ischecked: false,
      todolist:[],
      

    }
  },
  methods: {
    addList() {
      if(this.content === "" || this.content.match(/^[ ]*$/)){
        
        this.placeholder = "Don't null in this"
        this.color = "danger";
        setTimeout(()=>{
          this.placeholder = "Plase Input Something"
          this.color = "success";
        },500)
        
        return 
      }
      this.isround = !this.isround
      this.iscircle = !this.iscircle
      this.isloading = !this.isloading
      this.input = ""
      setTimeout(() => {
        console.log("enter")
        this.isround = !this.isround
        this.iscircle = !this.iscircle
        this.isloading = !this.isloading
        this.todolist.unshift({
          id:id++,
          content:this.content,
          completed:false
        })
        this.content = ""
        
      }, 300)
    },

  }
}

</script>
  

<style>
.el-card {
  margin-top: 5px;


}

.el-card__body {
  padding-top: 0;
  padding-bottom: 0;
}
</style>