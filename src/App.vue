<script lang="ts">
import Input from "./utils/Input.vue";
import Button from "./utils/Button.vue";
export default {
  components: {
    Input,
    Button,
  },
  data() {
    return {
      title: "Text-To-Speech App",
      input: "",
      count: "",
      lang: "",
      voices: [],
      status: "",
      synth: "",
      pending: false, 
    };
  },
  methods: {
    load(this: { voices: SpeechSynthesisVoice[]; synth: SpeechSynthesis }) {
      this.synth = speechSynthesis;
      const voices = this.synth.getVoices();
      this.voices = voices;
    },
    start(this: {
      voices: SpeechSynthesisVoice[];
      lang: SpeechSynthesisVoice;
      input: string;
      status: boolean;
      synth: SpeechSynthesis;
      pending: boolean
    }) {
      if(this.synth.pending){
        this.pending = this.synth.pending;
       return alert("Pening ...");
      }
      if (this.input.length > 1 && this.lang && this.synth) {
        const ss = new SpeechSynthesisUtterance(this.input);
        ss.voice = this.lang;
        this.status = this.synth.speaking;
        this.synth.speak(ss);
        this.status = this.synth.speaking;
        console.log("Start", this.synth.speaking)
      }
    },
    pause(this: { status: boolean; synth: SpeechSynthesis }) {
      if(this.synth){
        this.status = this.synth.speaking;
        this.synth.pause();
        this.status = this.synth.speaking;
        console.log("Pause", this.synth.paused);
      }
    },
    resume(this: { status: boolean; synth: SpeechSynthesis }) {
      if(this.synth){
        this.status = this.synth.speaking;
        this.synth.resume();
        this.status = this.synth.speaking;
        console.log("Resume", this.synth.speaking);
      }
    },
    cancel(this: { status: boolean; synth: SpeechSynthesis }) {
      if(this.synth){
        this.status = this.synth.speaking;
        this.synth.cancel();
        this.status = this.synth.speaking;
        console.log("cancled", this.synth.speaking);
      }
    },
  },
};
</script>

<template>
  <h1 class="ttl">{{ title }}</h1>
  <div class="mainBdy">
    <Input v-model="input" />
    <div>
      Status: <span v-if="pending">Pending</span><span v-else-if="status">Playing</span><span v-else>Paused</span>
    </div>
    <div class="btns">
      <select class="select" v-model="lang">
        <option v-for="voice in voices" class="option" :value="voice">
          {{ voice.name }}
        </option>
      </select>
      <Button color="crimson" txt="Load" :click="load"></Button>
      <Button color="crimson" txt="Start" :click="start"></Button>
      <Button color="#ffbe0b" txt="Pause" :click="pause"></Button>
      <Button color="#ffbe0b" txt="Resume" :click="resume"></Button>
      <Button color="#ffbe0b" txt="Cancel" :click="cancel"></Button>
    </div>
  </div>
</template>

<style>
* {
  background-color: aquamarine;
  width: 100%;
  padding: 0px;
  margin: 0px;
  box-sizing: border-box;
}

.ttl {
  padding: 1rem 0;
  text-align: center;
  font-size: 3rem;
  font-weight: bold;
  background-color: #2b2d42;
  color: white;
  text-decoration: underline;
  text-underline-offset: 10px;
  font-family: "Franklin Gothic Medium", "Arial Narrow", Arial, sans-serif;
}

.mainBdy {
  width: 80%;
  height: 100%;
  margin: auto;
}

.btns {
  margin: auto;
  width: max-content;
  padding: 0.5rem;
  background-color: pink;
  border: 2px solid #eee;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
}

.select {
  width: 100%;
  padding: 10px;
  border-radius: 5px;
  outline: none;
  cursor: pointer;
}

.select * {
  padding: 10px;
  font-size: 1rem;
}
</style>
