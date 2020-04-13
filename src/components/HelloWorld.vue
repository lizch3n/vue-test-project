<template>
    <div class="hello">
        <h1>Fragrance Finder</h1>
        <h4>simple vue app using vue cli <a href="//github.com/lizch3n/vue-test-project">github</a>
            <br/> => <a href="//fragrance-quiz-react.herokuapp.com/">react version</a></h4>
        <button v-on:click="reset">Reset</button>
        <ul>
            <template v-for="(question, i) in questions">
                <Question v-bind:key="i"
                          v-bind:i="i"
                          v-bind:question="question"
                          @clicked="onClickChild"
                          v-bind:check_this="checked(i)"
                          @changed="onOptionSelect"
                />
            </template>
        </ul>

        <div class="answerblock">
            <template v-for="(answer, i) in answers">
                <div v-bind:data="JSON.stringify(answer)" v-bind:key="key(i,'answer')">
                    <Answer v-bind:answer="answer"
                            v-bind:i="i"
                            v-bind:show="selectedAnswer(answer)"
                            v-bind:answered="questionAnswered()"
                            v-bind:class="{ show: selectedAnswer(answer), hide: !selectedAnswer(answer) }"
                    />
                </div>

            </template>


            <template v-if="showmsg">
                <h3>Answer some questions, or select below</h3>
            </template>
            <template v-for="(answer, i) in answers">
                <div v-bind:class="{ show: !selectedAnswer(answer), hide: selectedAnswer(answer) }"
                     v-bind:key="key(i,'options')">
                    <Options v-bind:answer="answer"
                             v-bind:i="i"
                             v-bind:show="selectedAnswer(answer)"
                             v-bind:answered="questionAnswered()"
                             v-bind:answers="answers"
                             @clicked="onClickOption"
                    />
                </div>
            </template>
        </div>
    </div>
</template>

<script>
    import Question from './Question.vue';
    import Answer from './Answer.vue';
    import Options from './Options.vue';

    let self;
    export default {
        name: 'HelloWorld',
        components: {
            Question,
            Answer,
            Options
        },
        props: {
            msg: String,
            questions: Array,
            answers: Array,
        },
        data: function () {
            self = this;
//            console.log(self);
            return {
                selected: new Array(10)
            }
        },
        methods: function () {
            const key = function (i, e) {
                return i + '_' + e
            };
            const onClickOption = function(val){
                const answer = self.answers.filter(function(obj){ return obj[val.val] });
                if (answer.length > 0) {
                    const selected = answer[0][val.val];
                    selected.forEach(function(arr,i){
                        self._data.selected.splice(i, 1, arr[0]);
                    })
                }
                onOptionSelect()
            }
            const onOptionSelect = function(v){
                console.log(v, 'onOptionSelect');
            }
            const onClickChild = function (value) {
//                console.log(value, 'child clicked') // someValue
                self._data.selected.splice(value.index, 1, value.val)
                selectedAnswer();
//                showmsg();

            }
            const questionAnswered = function () {
                return self._data.selected
            };
            const checked = function(index) {
                return self._data.selected[index];
            }
            const selectedAnswer = function (answer) {
                if (answer) {
                    const key = Object.keys(answer).filter(function (obj) {
                        return obj !== 'copy'
                    })[0];
                    const values = answer[key];
                    let truthy = [];
                    for (let i = 0; i < values.length; i++) {
                        truthy.push(values[i].indexOf(self._data.selected[i]) > -1 || values[i] == "");
                    }

                    return new Set(truthy).size == 1 && new Set(truthy).has(true);
                } else {
                    return false;
                }
            };
            const reset = function(){
                self._data.selected = new Array(10);
            }
            const showmsg = function(){
//                console.log('showmsg',self._data.selected.length, new Set(self._data.selected));
//                return new Set(self._data.selected).size == 1
            }
            return {
                key: key,
                onClickChild: onClickChild,
                selectedAnswer: selectedAnswer,
                questionAnswered: questionAnswered,
                onClickOption: onClickOption,
                checked: checked,
                onOptionSelect: onOptionSelect,
                reset:reset,
                showmsg: showmsg
            }
        }()
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    h3 {
        margin: 40px 0 0;
    }

    ul {
        width: 50%;
    }

    li {
        list-style-type: decimal;
        text-align: left;
    }

    a {
        color: #42b983;
    }

    .show {
        display: block;
    }

    .hide {
        display: none;
    }

    .answerblock {
        position: fixed;
        top: 20vh;
        right: 2em;
        width: calc(50vw - 4em);
    }
</style>
