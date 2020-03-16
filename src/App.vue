<template>
  <div id="main" class="h-100">
    <div class="container h-100">
      <div class="card h-100">
        <div class="card-header">
          <button class="btn btn-success float-right" v-on:click="newFile()" title="Novo arquivo">
            <i class="fa fa-plus"></i>
          </button>
          <h2>Note me senpai!</h2>
        </div>
        <div class="card-body h-100" style="padding: 0px;">
          <div class="row h-100">
            <div class="col-4 h-100 file-list">
              <div class="file-box" v-for="file in files" :key="file.id" v-on:click="setFile(file)">
                <h5 :key="file.title">{{file.title}}</h5>
                <span :key="file.content" class="file-content">{{file.content}}</span>
              </div>
            </div>
            <div class="col-8 file-edit">
              <input type="hidden" v-model="fle.id">
              <input type="text" class="form-control title-input" placeholder="Title" v-model="fle.title" v-on:change="interactFile()">
              <textarea class="text-editor" v-model="fle.content" v-on:change="interactFile(true)"></textarea>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import "bootstrap/dist/css/bootstrap.css";
import "font-awesome/css/font-awesome.css";

export default {
	name: 'App',
	data: function(){
		return {
			files: [{id: 1, title: "File 1", content: "Dude"},
				{id: 2, title: "File 2", content: "Quick"},
				{id: 3, title: "File 3", content: "Fella"},
				{id: 4, title: "File 4", content: "Son"},
				{id: 5, title: "File 5", content: "God"}
			],
			fle : {id: null, title: null, content: null}
		};
	},
	methods:{
		newFile(){
			this.fle.id = null;
			this.fle.title = null;
			this.fle.content = null;
		},
		setFile(f){
			this.fle.id = null;
			this.fle.title = null;
			this.fle.content = null;
			this.fle.id = f.id;
			this.fle.title = f.title;
			this.fle.content = f.content;
		},
		// setFileTitle(){
		// 	if(this.fle.id == null){
		// 		let id;
		// 		for(let f in this.files){
		// 			id = f.id;
		// 		}
		// 		this.fle.id = ++id;
		// 		this.files.push(this.fle);
		// 	} else {
		// 		for(let f in this.files){
		// 			if(this.fle.id == f.id){
		// 				f.title = this.fle.title;
		// 			}
		// 		}
		// 	}
		// },
		interactFile(descrip = false){
			if(this.fle.id == null){
				let id;
				for (let i = 0; i < this.files.length; i++) {
					const f = this.files[i];
					id = f.id;
				}
				this.fle.id = ++id;
				this.files.push(this.fle);
			} else {
				let idx;
				for (let i = 0; i < this.files.length; i++) {
					const f = this.files[i];
					if(this.fle.id == f.id){
						idx = this.files.indexOf(f);
					}
				}
				this.files.splice(idx,1);
				this.files.push({id: this.fle.id, title: this.fle.title, content: this.fle.content,});
			}
			if(descrip)
				this.fle = {id: null, title: null, content: null};
		}
	},
};
</script>

<style>
  html,body{
    height: 100%;
  }
  
  #main{
    height: 100%;
    padding: 20px;
  }

  textarea{
    resize: none;
  }

  .text-editor{
    width: 100%;
    height: 100%;
    border: 0px;
  }

  .file-box{
    width: 100%;
    padding: 5px;
    border-width: 0px 0px 1px 0px;
    border-style: solid;
    border-color: #d5d5d5;
  }

  .file-list{
    padding-right: 0px;
    overflow: auto;
    border-width: 0px 1px 0px 0px;
    border-style: solid;
    border-color: #d5d5d5;
  }

  .file-edit{
    padding-left: 0px;
  }

  .file-content{
    overflow: hidden;
    text-overflow: ellipsis;
    display: -webkit-box;
    -webkit-line-clamp: 2; /* number of lines to show */
    -webkit-box-orient: vertical;
  }

  .title-input{
    border-radius: 0px;
    border-width: 0px 0px 1px 0px;
  }
</style>
