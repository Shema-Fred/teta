<template>
  <section class="bg-dark text-light py-5">
    <b-container class="">
      <b-row>
        <b-col cols="12" md="6" lg="6">
          <b-form @submit.prevent="send" class="pr-0 pr-md-3 pr-lg-4">
            <b-form-group>
              <b-input
                v-model="name"
                trim
                required
                placeholder="What's your name?"
                class="bg-dark border-light text-light input"
              />
            </b-form-group>
            <b-form-group>
              <b-input
                type="email"
                class="bg-dark border-light text-light input"
                trim
                required
                v-model="email"
                placeholder="What's your email?"
              />
            </b-form-group>
            <b-form-group>
              <b-textarea
                trim
                v-model="message"
                required
                placeholder="Tell me something"
                class="bg-dark border-light text-light input"
              ></b-textarea>
            </b-form-group>
            <b-form-group>
              <b-button block variant="light" type="submit">
                <span v-if="state.loading">
                  <b-spinner small />
                </span>
                <span v-else>SEND</span>
              </b-button>
            </b-form-group>
          </b-form>
        </b-col>
        <b-col cols="12" md="3" lg="2">
          <h5 class="mb-3">QUICK LINKS</h5>
          <ul class="list-group">
            <li class="list-item">
              <b-link>Home</b-link>
            </li>
            <li class="list-item">
              <b-link>Gallery</b-link>
            </li>
            <li class="list-item">
              <b-link>Timeline</b-link>
            </li>
            <li class="list-item">
              <b-link>About</b-link>
            </li>
            <li class="list-item">
              <b-link>My Bio</b-link>
            </li>
          </ul>
        </b-col>
        <b-col cols="12" md="3" lg="4">
          <b-row align-h="end" align-v="center" class="mb-4">
            <div class="logo-box rounded text-primary">TETA CHEL</div>
          </b-row>
          <b-row align-h="end" class="mb-4">
            <h6>Contact: <a href="tel:+250789547667">(+250) 789 547 667</a></h6>
            <h6>
              Email:
              <a href="mailto:michelineteta@gmail.com"
                >michelineteta@gmail.com</a
              >
            </h6>
          </b-row>
          <b-row align-h="end">
            <h6>Ending on 25.09.2021</h6>
          </b-row>
          <b-row align-h="end">
            <b-col cols="1">
              <a
                href="https://web.facebook.com/teta.micheline"
                target="_blank"
                class="text-light"
                ><b-icon-facebook
              /></a>
            </b-col>
            <b-col cols="1">
              <a
                href="https://www.instagram.com/teta_chel"
                target="_blank"
                class="text-light"
              >
                <b-icon-instagram
              /></a>
            </b-col>
            <b-col cols="1">
              <a
                href="https://twitter.com/tetachel"
                target="_blank"
                class="text-light"
                ><b-icon-twitter
              /></a>
            </b-col>
            <b-col cols="1">
              <a
                href="https://www.youtube.com/channel/UCyTGn98Cpr0_ptkEu3nvAeA"
                target="_blank"
                class="text-light"
              >
                <b-icon-youtube
              /></a>
            </b-col>
          </b-row>
        </b-col>
      </b-row>
    </b-container>
  </section>
</template>

<script>
export default {
  data() {
    return {
      state: { loading: false },
      name: null,
      email: null,
      message: null,
    };
  },
  methods: {
    async send() {
      try {
        this.state.loading = true;
        const data = await this.axios.post(
          "https://api.emailjs.com/api/v1.0/email/send",
          {
            user_id: "user_JO6leZ9m5OppROqiYcZHT",
            service_id: "service_tga6eg8",
            template_id: "template_9bhgofi",
            template_params: {
              name: this.name,
              email: this.email,
              message: this.message,
            },
          }
        );
        console.log(data);
      } catch (err) {
        console.log(err);
      } finally {
        this.state.loading = false;
      }
    },
  },
};
</script>

<style lang="scss" scoped>
.input,
textarea {
  &::placeholder {
    color: #a7adb9fc !important;
  }
}
.list-item {
  list-style: none;
  padding: 5px 4px;
  font-size: 17px;

  a {
    color: var(--light);
    &:hover {
      text-decoration: none;
      opacity: 0.7;
    }
  }
}
.logo-box {
  background-color: black;
  height: 100px;
  width: 115px;
  text-align: center;
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>