<template>
  <div>

    <header class="header editor-header">
      <div class="left-box">

      </div>
      <input maxlength="20" placeholder="请输入标题..." spellcheck="false"
             class="title-input title-input"/>
      <div class="right-box">

        <div data-v-98c9024a="" data-v-c5c24ff2="" title="最近保存于 2021/7/11上午10:05:31"
             class="status-text status-text with-padding">保存成功
        </div>
        <button data-v-c5c24ff2="" class="xitu-btn with-padding xitu-btn-outline"> 草稿箱</button>
        <div class="publish-popup with-padding">
          <button data-v-c5c24ff2="" class="xitu-btn   "> 发布</button>
        </div>
        <nav class="navigator main-navigator with-padding">
          <div data-v-93577b52="" class="toggle-btn"
               style="background-image: url(&quot;https://user-gold-cdn.xitu.io/2019/9/2/16cf179cdba75bef?imageView2/1/w/64/h/64/q/85/interlace/1&quot;);"></div>
        </nav>

        <!--        <button>主动保存</button>-->
      </div>

    </header>

    <!--    <div style="padding: 10px 0;">-->
    <!--      Plugins:-->
    <!--      <label v-for="p in Object.keys(enabled)" :key="p">-->
    <!--        <input-->
    <!--            type="checkbox"-->
    <!--            :checked="enabled[p]"-->
    <!--            @change="handlePluginChange($event, p)"-->
    <!--        />-->
    <!--        {{ p }}-->
    <!--      </label>-->
    <!--    </div>-->

    <Editor
        :value="value"
        @change="handleChange"
        :plugins="enabledPlugins"
        class="main"
    />


  </div>
</template>

<script>
import 'github-markdown-css';
import 'highlight.js/styles/vs.css';
import 'katex/dist/katex.css';
import 'bytemd/dist/index.css';
import 'bytemd/dist/index.min.css';
import {Editor, Viewer} from '@bytemd/vue';
import highlight from '@bytemd/plugin-highlight';
import math from '@bytemd/plugin-math';
// import mermaid from '@bytemd/plugin-mermaid';

export default {
  components: {
    Editor,
    // eslint-disable-next-line vue/no-unused-components
    Viewer,
  },
  data() {
    return {
      value: '',
      enabled: {
        highlight: true,
        math: true,
        mermaid: true,
      },
    };
  },
  computed: {
    enabledPlugins() {
      return [
        this.enabled.highlight && highlight(),
        this.enabled.math && math(),
        // mermaid: enabled.mermaid && mermaid(),
      ];
    },
  },
  methods: {
    handleChange(v) {
      this.value = v;
    },
    handlePluginChange($event, p) {
      this.enabled[p] = $event.target.checked;
    },
  },
  async mounted() {
    const res = await fetch(
        'https://raw.githubusercontent.com/bytedance/bytemd/main/assets/demo.md'
    );
    const text = await res.text();
    this.value = text;
  },
};
</script>

<style>
body {
  margin: 0px;
}

.bytemd {
  height: 90vh !important;
}

.title-input {
  margin: 0;
  padding: 0;
  font-size: 24px;
  font-weight: 500;
  border: none;
  outline: none;
  color: #1d2129;
}

.title-input {
  flex: 1 1 auto;
  height: 100%;
}

header {
  display: flex;
  /*position: fixed;*/
  top: 0;
  left: 0;
  right: 0;
  padding: 0 27px;
  height: 5.334rem;
  background-color: #fff;
  border-bottom: 1px solid #ddd;
  z-index: 100;
}

html {
  color: #333;
  font-family: -apple-system, system-ui, BlinkMacSystemFont, Helvetica Neue, PingFang SC, Hiragino Sans GB, Microsoft YaHei, Arial, sans-serif;
  font-size: 12px;
  line-height: 1.2;
  text-rendering: optimizeLegibility;
}

.right-box {
  display: flex;
  -webkit-box-align: center;
  -ms-flex-align: center;
  align-items: center;

  -webkit-box-pack: end;
  -ms-flex-pack: end;
  justify-content: flex-end;
}

.status-text {
  font-size: 14px;
  white-space: nowrap;
  color: #c9cdd4;
  cursor: default;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.with-padding {
  margin-left: 8px;
  margin-right: 8px;
}

.xitu-btn {
  height: 32px;
  padding: 2px 16px;
  font-size: 14px;
  line-height: 22px;
  border: 1px solid #1d7dfa;
  border-radius: 2px;
  cursor: pointer;
  color: #fff;
  -webkit-box-sizing: border-box;
  box-sizing: border-box;
  background-color: #1d7dfa;
}

.xitu-btn-outline {
  color: #1d7dfa;
  background-color: #fff;
}
.toggle-btn {
  width: 2.667rem;
  height: 2.667rem;
  border-radius: 50%;
  background-color: #eee;
  background-position: 50%;
  background-size: cover;
  background-repeat: no-repeat;
  cursor: pointer;
}
</style>
