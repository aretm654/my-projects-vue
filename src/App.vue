<script>
import MatrixBackground from './components/MatrixBackground.vue'
import Header from './components/Header.vue';
import Project from './components/Project.vue';

export default {
  components: {
    MatrixBackground,
    Header,
    Project
  },
  data() {
    return {
      loading: true,
      projects: []
    };
  },
  async created() {

  },
};
</script>

<template>
  <MatrixBackground lineCount="6" speed="3" cellSize="40" lineColor="#ffffff" lineThickness="1" />
  <div class="content">
    <Header></Header>
  <Project style="margin-top: 70px;" link="www.google.com" photo="https://cdn-dynmedia-1.microsoft.com/is/image/microsoftcorp/Blade001_Hero_960x675_Transparent_2x?resMode=sharp2&op_usm=1.5,0.65,15,0&wid=1920&qlt=100&fmt=png-alpha&fit=constrain" text="крутой ттекст" />
  <Project style="margin-top: 20px;" link="www.google.com" photo="https://cdn-dynmedia-1.microsoft.com/is/image/microsoftcorp/Blade001_Hero_960x675_Transparent_2x?resMode=sharp2&op_usm=1.5,0.65,15,0&wid=1920&qlt=100&fmt=png-alpha&fit=constrain" text="крутой ттекст" />
  </div>
</template>

<style>
  html, body, div, span, applet, object, iframe,
  h1, h2, h3, h4, h5, h6, p, blockquote, pre,
  a, abbr, acronym, address, big, cite, code,
  del, dfn, em, img, ins, kbd, q, s, samp,
  small, strike, strong, sub, sup, tt, var,
  b, u, i, center,
  dl, dt, dd, ol, ul, li,
  fieldset, form, label, legend,
  table, caption, tbody, tfoot, thead, tr, th, td,
  article, aside, canvas, details, embed, 
  figure, figcaption, footer, header, hgroup, 
  menu, nav, output, ruby, section, summary,
  time, mark, audio, video {
    margin: 0;
    padding: 0;
    border: 0;
    font-size: 100%;
    font: inherit;
    vertical-align: baseline;
  }
  /* HTML5 display-role reset for older browsers */
  article, aside, details, figcaption, figure, 
  footer, header, hgroup, menu, nav, section {
    display: block;
  }
  body {
    line-height: 1;
  }
  ol, ul {
    list-style: none;
  }
  blockquote, q {
    quotes: none;
  }
  blockquote:before, blockquote:after,
  q:before, q:after {
    content: '';
    content: none;
  }
  table {
    border-collapse: collapse;
    border-spacing: 0;
  }

  p {
    color: white
  }
</style>