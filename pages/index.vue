<template>
  <div class="container">
    <div class="header">
      <header class="site-header">
        <div class="wrapper site-header__wrapper">
          <a href="#" class="brand">Hime's portfolio</a>
          <nav class="nav">
            <ul class="nav__wrapper">
              <li class="nav__item"><a href="#">About</a></li>
              <li class="nav__item"><a href="#">Picture</a></li>
              <li class="nav__item"><a href="#">Contact</a></li>
            </ul>
          </nav>
        </div>
      </header>
      <div>
        <b-carousel
          id="carousel-1"
          v-model="slide"
          :interval="4000"
          controls
          indicators
          background="#ababab"
          img-width="1024"
          img-height="480"
          style="text-shadow: 1px 1px 2px #333;"
          @sliding-start="onSlideStart"
          @sliding-end="onSlideEnd"
        >
          <!-- Text slides with image -->
          <b-carousel-slide
            caption="First slide"
            text="Nulla vitae elit libero, a pharetra augue mollis interdum."
            img-src="https://picsum.photos/1024/480/?image=52"
          ></b-carousel-slide>
          <b-carousel-slide img-src="https://picsum.photos/1024/480/?image=54">
            <h1>Hello world!</h1>
          </b-carousel-slide>
          <b-carousel-slide img-src="https://picsum.photos/1024/480/?image=58"></b-carousel-slide>
          <b-carousel-slide img-src="https://picsum.photos/1024/480/?image=55"></b-carousel-slide>
        </b-carousel>
      </div>
      <h3>
        About
      </h3>
      <p>
        2000年生まれ
        秋田出身
      </p>
      <h3>
        picture
        <div class="recentpicture">
          <img
            src="data:image/jpeg;base64,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">
          <img
            src="https://encrypted-tbn0.gstatic.com/images?q=tbn%3AANd9GcSQ2RTNGX70WKDV0i6o7UYbr1LKsjLaUVh6aQ&usqp=CAU">
        </div>
      </h3>
      <h3>
        contact
      </h3>
      <div class="contact">
        <a
          href="https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=&cad=rja&uact=8&ved=2ahUKEwjkp4GGlIHsAhVaa94KHatEAAIQFjAAegQIAxAB&url=https%3A%2F%2Fwww.instagram.com%2Fpiyo_1_2%2F&usg=AOvVaw0HPIu66kw31JVZG9fNWzPQ">
          <img src="https://rakugakiicon.com/ri/wp-content/uploads/2018/11/instagram.png" height="50px" width="50px">
        </a>
        <a
          href="https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=&ved=2ahUKEwj4tvzZk4HsAhXJUN4KHXjnDZEQFjAAegQIAhAB&url=https%3A%2F%2Ftwitter.com%2Fpiyo_1_2&usg=AOvVaw2B5GIMFsI4JaurweCURe87">
          <img
            src="https://rakugakiicon.com/ri/wp-content/uploads/2015/04/e31d3d5320e34c64622d3bd7f4c80000.png"
            height="50px"
            width="50px">
        </a>
      </div>
    </div>
  </div>
</template>
<script>

export default {
  data () {
    return {
      slide: 0,
      sliding: null
    }
  },
  methods: {
    onSlideStart (slide) {
      this.sliding = true
    },
    onSlideEnd (slide) {
      this.sliding = false
    }
  }
}
</script>

<style>
.container {
  background-color: lavender;
}

.title {
  font-family: 'Quicksand',
  'Source Sans Pro',
  -apple-system,
  BlinkMacSystemFont,
  'Segoe UI',
  Roboto,
  'Helvetica Neue',
  Arial,
  sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}

ul {
  list-style: none;
  padding-top: 1rem;
  padding-bottom: 0;
  padding-right: 20px;
}

.nav__wrapper {
  display: flex;
}

.site-header__wrapper {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding-top: 0;
  padding-bottom: 0;
}

.nav__item {
  padding-right: 20px;
  color: white;
  text-decoration: none;
}

.brand {
  font-weight: bold;
  font-size: 20px;
  padding-left: 20px;
}

h3 {
  justify-content: center;
  align-items: center;
  text-align: center;
  margin-top: 20px;
}

.recentpicture {
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  margin-top: 10px;
}

.contact {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;
}
p{
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;
}
</style>
