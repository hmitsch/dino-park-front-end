<template>
  <div id="app" class="app-container">
    <TopBar></TopBar>
    <RouterView />
    <Footer></Footer>
  </div>
</template>

<script>
import TopBar from '@/components/ui/TopBar.vue';
import Footer from '@/components/ui/Footer.vue';

import isDNTEnabled from '@/assets/js/dnt-enabled';

export default {
  name: 'PageHome',
  components: {
    TopBar,
    Footer,
  },
  methods: {
    awaitTabbing() {
      document.addEventListener('keydown', (e) => {
        if (e.key === 'Tab') {
          document.body.classList.add('focus-styles');
        }
      });
    },
    loadGA() {
      const dntEnabled = isDNTEnabled();
      const googleId = 'GTM-5GCB5DL';

      if (dntEnabled === false) {
        const firstScriptTag = document.querySelector('script');
        const newTag = document.createElement('script');

        window.dataLayer = window.dataLayer || [];
        window.dataLayer.push({
          'gtm.start': new Date().getTime(),
          event: 'gtm.js',
        });

        newTag.async = true;
        newTag.src = `https://www.googletagmanager.com/gtm.js?id=${googleId}`;

        firstScriptTag.parentNode.insertBefore(newTag, firstScriptTag);
      }
    },
  },
  mounted() {
    this.awaitTabbing();
    this.loadGA();
  },
};
</script>

<style>
:root {
  --gray-10: #f9f9fa;
  --gray-20: #ededf0;
  --gray-30: #d7d7db;
  --gray-40: #b1b1b3;
  --gray-50: #737373;
  --gray-60: #4a4a4f;
  --blue-60: #0060df;
  --white: #fff;
  --black: #000;

  --lightBlue: #f2fcfd;
  --transparentBlue: rgba(69, 161, 255, 0.54);
  --transparentWhite: rgba(255, 255, 255, 0.54);

  --layerOne: 1;
  --layerTwo: 2;
  --layerThree: 3;
  --layerTopBar: 4;
  --layerProfileNav: 5;
  --layerContactMe: 6;
  --layerAboveNav: 7;
  --layerUserMenu: 8;
  --layerModal: 9;

  --shadowCard: 0 0.25em 0.25em 0 rgba(210, 210, 210, 0.5);

  --imageRadius: 0.25em;
  --formElementRadius: 0.25em;
  --cardRadius: 0.125em;
}

@media (min-width: 57.5em) {
  :root {
    --layerProfileNav: 4;
    --layerContactMe: 5;
    --layerTopBar: 6;
  }
}

* {
  box-sizing: border-box;
}

body {
  background: var(--gray-20);
  font-family: 'Open Sans', sans-serif;
  scroll-behavior: smooth;
  margin: 0;
  font-size: 87.5%;
  letter-spacing: 0.04em;
}

h1,
h2,
h3,
h4,
h5,
h6 {
  margin-top: 0;
}

h1 {
  font-family: 'Zilla Slab', sans-serif;
  font-weight: 400;
  font-size: 2.5em;
}
@media (min-width: 57.5em) {
  h1 {
    font-size: 3.5em;
  }
}

h2 {
  font-weight: 400;
  font-size: 1.5em;
  margin-bottom: 0.5em;
}

h3 {
  font-weight: 700;
  font-size: 1em;
  color: var(--black);
}

h4,
h5 {
  font-size: 1em;
}

img,
pre,
audio,
video,
section {
  max-width: 100%;
  overflow: auto;
}

hr {
  border: 0;
  height: 1px;
  background-color: var(--gray-30);
  margin: 2em 0;
}

a {
  color: var(--blue-60);
}
a:hover {
  color: var(--black);
}

button {
  cursor: pointer; /* as per issue #50 :'( */
}

.container {
  padding: 0 1em;
  width: 100%;
}
@media (min-width: 57.5em) {
  .container {
    max-width: 74em;
    margin: 0 auto;
  }
}

.app-container {
  display: grid;
  grid-template-rows: auto 1fr auto; /* this assumes an app container with:; header, content, footer; it makes header and footer as tall as they need to be, then gives remaining whitespace to content.  */
  min-height: calc(100vh - 5.5em);
  align-items: center; /* if there is not enough content, that content will center in the available space */
}
.app-container > * {
  min-width: 0; /* ‘auto’ is default for grid children,
      but that would break our responsiveness in this case */
}
.app-container > footer {
  grid-row: 4 / 5;
}

.visually-hidden {
  border: 0;
  clip: rect(0 0 0 0);
  width: 1px;
  height: 1px;
  margin: -1px;
  overflow: hidden;
  padding: 0;
  position: absolute;
  white-space: nowrap;
}

/* best only use these classes on elements that
     do not have anything else, we don't want it
     to interfere with other display values */
.hide-mobile {
  display: none;
}
@media (min-width: 57.5em) {
  .hide-mobile {
    display: initial;
  }
  .hide-desktop {
    display: none;
  }
}

:focus {
  outline: none;
}
::-moz-focus-inner {
  border: 0;
}
.focus-styles :focus {
  outline: none;
  box-shadow: 0px 0 0 1px var(--blue-60), 0 0 0 3px var(--transparentBlue);
}
.focus-styles ::-moz-focus-inner {
  border: 0;
}
.focus-styles :focus:not(:focus-visible) /* don't show focus if element didn't gain focus by means of keyboard  */ {
  box-shadow: none;
}

[tabindex='-1']:focus,
.focus-styles [tabindex='-1']:focus {
  outline: none; /* if tabindex is -1, focus was
    set programmatically to something that is usually
    not focused (ie not an interactive element), in
    order to improve reading order in widgets; no
    outline seems sensible as it usually concerns
    large elements that people would not expect to
    have focus. */
  box-shadow: none;
}

.actions ul {
  display: grid;
  grid-gap: 1em;
  grid-auto-flow: column;
  grid-auto-columns: 1fr;
  padding: 0;
  margin: 0;
}
.actions li {
  list-style: none;
}
.actions button {
  display: block;
  width: 100%;
}
</style>
