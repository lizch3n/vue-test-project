<template>
    <li>
       {{ question.question }}
       <template v-for="(answer,inx) in question.answers">
           <div v-bind:key="answer+inx" >
                <input type="radio"
                    :id="id(i,Object.keys(answer)[0])"
                    :name="name(i)"
                    :value="Object.keys(answer)[0]"
                    :index="i"
                    v-on:change="checked"
                    v-bind:checked="selectedthis(Object.keys(answer)[0])"
                />
                <label v-bind:for="id(i,Object.keys(answer)[0])" v-bind:test="inx">
                    {{Object.keys(answer)[0]}}: {{Object.values(answer)[0]}}
                </label>
            </div>
       </template>
    </li>
</template>

<script>
let self;
export default {
  name: 'Question',
  props: {
    msg: String,
    question: Object,
    i: Number
  },
  data: function(){
    self = this;
    return {
        selected: ""
    }
  },
  methods: function(){
    const checked = function(evt){
        self._data.selected = evt.target.value;
        this.$emit('clicked', {"val":evt.target.value, "index":evt.target.getAttribute('index')});
    }
    const name = function(str) {
        return "question_"+str;
    }
    const id = function(i,o) {
            return i+'_'+o;
    }
    const selectedthis = function(val){
//        console.log(self, self.$attrs.check_this);
        return self.$attrs.check_this == val ;
    }
    return {
        checked: checked,
        name: name,
        id: id,
        selectedthis: selectedthis
    }
  }(this)
}
</script>