<template>
  <div
    id="app"
    class="page-wrapper">

    <div class="content-wrapper">
      <monarch-navbar/>
      <div class="main-wrapper">
        <router-view/>
      </div>
    </div>

    <div class="footer-wrapper">
      <monarch-footer
        :compact="useCompactFooter"/>
    </div>

  </div>
</template>

<script>
import Vue from 'vue';
import Navbar from '@/components/Navbar.vue';
import Footer from '@/components/Footer.vue';
import sanitizeHTML from 'sanitize-html';

Vue.prototype.$sanitizeText = function sanitizeText(dirty) {
  const result = sanitizeHTML(dirty, {
    allowedTags: sanitizeHTML.defaults.allowedTags.concat(['img', 'sup'])
  });

  return result;
};

Vue.component('monarch-footer', Footer);
export default {
  name: 'App',
  components: {
    'monarch-navbar': Navbar
  },
  data() {
    return {
      useCompactFooter: false,
    };
  },
  watch: {
    '$route': function $route(to, from) {
      this.useCompactFooter = (to.path !== '/');
    }
  },
  mounted() {
    this.useCompactFooter = (this.$route.path !== '/');
  },
};

</script>

<style lang="scss">
@import "~@/style/variables.scss";

$fa-font-path: "~font-awesome/fonts" !default;
@import '~font-awesome/scss/font-awesome';
@import "~bootstrap/scss/bootstrap";
@import '~bootstrap-vue/dist/bootstrap-vue.css';

[v-cloak] {
  display: none;
}

// https://medium.freecodecamp.org/how-to-keep-your-footer-where-it-belongs-59c6aa05c59c

#app.page-wrapper {
  position: absolute;
  min-height: 100vh;
  width: 100%;
}

#app.page-wrapper .content-wrapper {
  padding-bottom: $footer-height;
  margin: 0;
}

#app.page-wrapper .footer-wrapper {
  position: absolute;
  z-index: $monarch-footer-z;
  bottom: 0;
  width: 100%;
  height: $footer-height;
  padding: 0;
  margin: 0;
}

.monarch-view {
  padding-top: 15px;
}

#app.page-wrapper .main-wrapper {
  padding: $navbar-height 15px;
}


div.vue-markdown {
  xmargin-top: $navbar-height;
  xborder: 5px solid cyan;
}

div.container-fluid.monarch-home-view div.vue-markdown,
div.container-fluid.monarch-view div.vue-markdown {
  margin-top: 0;
  xborder: 5px solid magenta;
}

div.vue-markdown-plain {
  margin-top: $navbar-height;
  padding: 20px;
  xborder: 5px solid lightgreen;

  pre {
    background-color: #f6f8fa;
    border-radius: 3px;
    font-size: 85%;
    line-height: 1.45;
    overflow: auto;
    padding: 16px;

    code {
      background-color: unset;
      border-radius: unset;
      color: unsete;
      background-color: unset;
      border-radius: unset;
      font-size: unset;
      margin: unset;
      padding: unset;
    }
  }

  code {
    background-color: #f6f8fa;
    border-radius: 3px;
    color: #24292e;
    background-color: rgba(27,31,35,.05);
    border-radius: 3px;
    font-size: 85%;
    margin: 0;
    padding: .2em .4em;
  }
}


:target::before {
  content: "";
  display: block;
  height: $navbar-height; /* fixed header height*/
  margin: -$navbar-height 0 0; /* negative fixed header height */
}

a.header-anchor {
  vertical-align: middle;
  font-size: 0.6em;
  opacity: 0;
  padding-top: 90px;
}

a.header-anchor, a.header-anchor:hover, .title a {
  text-decoration: none;
}

h1:hover a.header-anchor, h2:hover a.header-anchor, h3:hover a.header-anchor,
h4:hover a.header-anchor, h5:hover a.header-anchor, h6:hover a.header-anchor {
  opacity: 1;
}

blockquote.blockquote {
  padding: 4px 4px 0 8px;
  font-size: ($font-size-base * 1.1);
  border-radius: 5px;
  border-left: 2px solid lightgray;
}

</style>
