<template>
  <footer id="footer">
    <p>Make Your Burger &copy; 2023</p>

    <div id="footer-icons">
      <img
        @click="accessLink($event)"
        src="../../public/img/icons/github.svg"
        :data-link="link_git"
        alt="GitHub"
        class="icons"
      />

      <img
        @click="accessLink($event)"
        src="../../public/img/icons/linkedin.svg"
        :data-link="link_linkedin"
        alt="LinkedIn"
        class="icons"
      />
    </div>
  </footer>
</template>

<script>
export default {
  name: 'Footer',
  data() {
    return{
        link_git: 'https://github.com/franciscograveli/franciscograveli',
        link_linkedin: 'https://www.linkedin.com/in/francisco-carlos-609192142/'
    }
  },
  methods: {
    accessLink(event) {
      const link = event.target.getAttribute('data-link');
      if (link) {
        window.open(link, '_blank');
      }
    },
  },
};
</script>

<style scoped>
#footer {
  background-color: #222;
  text-align: center;
  height: 200px;
  border-top: #111 4px solid;
  color: #fcba03;
  display: flex;
  justify-content: center;
  align-items: center;
  bottom: 0;
  width: 100%;
  display: flex;
  flex-direction: column;
}

#footer-icons{
  margin-top: .5rem !important;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: row;
  flex-wrap: wrap;
}

img {
    margin: 0rem .5rem !important;
  width: 36px;
  height: 36px;
  filter: drop-shadow(0px 0px 1px #fcba0315);
}

img:hover {
  filter: drop-shadow(0px 0px 5px #fcba03);
  cursor: pointer;
}
</style>
