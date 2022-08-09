<template>
      <div>
            <b-navbar toggleable="lg" type="dark" variant="dark">
                  <b-navbar-brand id="logo" href="#">
                        <h3 class="text-dark">Question & answer</h3>
                  </b-navbar-brand>

                  <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

                  <b-navbar-nav>
                        <b-nav-item class="bg-dark rounded"> Question {{ index }}/10 </b-nav-item>
                        <b-nav-item href="#" disabled></b-nav-item>
                  </b-navbar-nav>
                  <b-navbar-nav>
                        <b-nav-item class="bg-dark rounded"> CorrectAnswers : {{ correctAnswers }} </b-nav-item>
                        <b-nav-item href="#" disabled></b-nav-item>
                  </b-navbar-nav>
            </b-navbar>
      </div>
</template>

<script>
export default {
      name: "Q&Aheader",
      props: {
            index: Number,
            correctAnswers: Number,
      },
};
</script>

<style>
#bg-list {
      background-color: rgb(255, 68, 0);
}
#logo {
      background-color: rgb(255, 226, 6);
      border-radius: 5px;
      padding: 5px;
}
</style>
