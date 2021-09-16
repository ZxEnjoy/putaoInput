<template>

        <div contenteditable="plaintext-only" @blur="check" @focus="uncheck" 
        @compositionend="compositionend"    @keydown="keydown"  @compositionstart="start" @keyup="keyup"
        class="io" :class="{placeholder:gray}" :style="{'min-width':min_width+'px'}">
        </div>
        
</template>

<script>
function insert_string(old_str,new_str,max){
    const old_ln=old_str.length
    let add_number = max - old_ln;
    let res=''
    //当在old_str中间插入 则遍历可得不同的地方
    for(let i=0;i<old_ln;i++){ 
        if(old_str[i]!==new_str[i]){
            //add new
            for(let j = i;j<(i+add_number);j++){
                console.log('new')
                res+=new_str[j]
            }
            //add old
            for(let j = i;j<old_ln;j++){
                console.log('old')
                res+=old_str[j]
            }
            console.log(res)
            return res
        }
        res+=old_str[i]
    }
    //制空
    res=''
    //未遍历到则说明插入在尾部
    for(let i=0;i<max;i++){
        res+=new_str[i]
    }

    return res;
}
function str_head(str,max){
    let res='';
    for(let i=0;i<max;i++){
        res+=str[i]
    }
    return res;
}
export default {
    name: 'x-input',
    mounted(){
        this.init = false
        this.$el.onkeypress = (e)=>{
            if(this.$el.textContent.length>=this.maxlength){
                //if(e.key!=='Enter') 
                e.returnValue=false}
        }
        if(this.disabled==='disabled'){
            this.$el.contentEditable= false
        }
        //console.log(this.$el.style.min-width)
    },
    props:{
        placeholder:{
            type:String
        },
        maxlength:{
            type:Number
        },
        disabled:{
            type:String
        },
        min_width:{
            type:Number
        }
    },
    data(){
        return{
            init:true,
            gray:true,
            oldvalue:'',
            newvalue:''
        }
    },
    watch:{
        init(newinit){
            if(!newinit){
                this.$el.textContent=this.placeholder
                this.gray=true
            }else{
                this.gray=false
            }
        }
    },
    methods:{
        check:function(event){
            if(event.target.textContent.length===0){
                this.init = false
            }else{
                this.init = true
            }
        },
        uncheck:function(){
            if(!this.init){
                this.$el.textContent=""
            }
            this.init = true;
        },
        compositionend:function(e){
            this.newvalue = this.$el.textContent
            if(this.newvalue.length>this.maxlength&&this.oldvalue.length<this.maxlength){
                this.$el.textContent=insert_string(this.oldvalue,this.newvalue,this.maxlength)
            }else if(this.oldvalue.length>this.maxlength){
                this.$el.textContent = str_head(this.oldvalue)
            }else if(this.oldvalue.length===this.maxlength){
                this.$el.textContent = this.oldvalue
            }
            
        },
        keydown:function(e){
            if(e.key==='v'||e.key==='V'&&e.ctrlKey){
                this.oldvalue = this.$el.textContent
                
            }
        },
        keyup:function(e){
            if(e.key==='v'||e.key==='V'&&e.ctrlKey){
                this.newvalue = this.$el.textContent

                            if(this.newvalue.length>this.maxlength&&this.oldvalue.length<this.maxlength){
                this.$el.textContent=insert_string(this.oldvalue,this.newvalue,this.maxlength)
            }else if(this.oldvalue.length>this.maxlength){
                this.$el.textContent = str_head(this.oldvalue)
            }else if(this.oldvalue.length===this.maxlength){
                this.$el.textContent = this.oldvalue
            }
            }
            this.$emit('input',this.$el.textContent)
        },
        start:function(e){
            this.oldvalue = this.$el.textContent
        }
    }

}
</script>
<style scoped>
*{
    outline:none;
}
.io{
    display: inline-block;
    border: 2px solid rgb(43,151,240);
    min-width: 300px;
    padding: 4px 8px;
}
.placeholder{
    color: rgb(102,102,102);
}
</style>
