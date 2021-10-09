<template>
    <div class="hero-carousel">
        <div class="slide-container">
            <div class="animation-wrap">
               
                <div v-if="runAnimation" class="slide previous"
                    :class="isNext != null ? isNext ? 'nextOne' : 'previousOne' : ''"
                    :style="{ 
                        backgroundImage: `url(${require(`@/assets/${list[
                            isNext ? nextIndex : activeIndex
                        ].image}`)})`,
                    }"
                ></div>
                
                <div v-if="runAnimation" class="slide next"
                    :class="isNext != null ? isNext ? 'nextThree' : 'previousThree' : ''"
                    :style="{ 
                        backgroundImage: `url(${require(`@/assets/${list[
                            isNext ? activeIndex : previousIndex
                        ].image}`)})`,
                    }"
                ></div>

                <div v-if="runAnimation" class="slide current"
                    :class="isNext != null ? isNext ? 'nextTwo' : 'previousTwo' : ''"
                    :style="{ 
                        backgroundImage: `url(${require(`@/assets/${list[
                            isNext ? previousIndex : nextIndex
                        ].image}`)})`,
                    }"
                ></div>
                 <div v-if="!runAnimation" class="slide"
                    :style="{ 
                        backgroundImage: list[activeIndex] ? `url(${require(`@/assets/${list[activeIndex].image}`)})` : '',
                    }"
                ></div>
            </div>
        </div>

        <div v-if="list.length && loaded" class="text-container">
            <div v-if="list[activeIndex]" class="text-title">
                <h2 v-if="list[activeIndex].title">{{ list[activeIndex].title }}</h2>
            </div>
            <br/>
            <div v-if="list[activeIndex]" class="text-description">
                <p v-if="list[activeIndex].text">{{ list[activeIndex].text }}</p>
            </div>
            <br/>
            <div v-if="list[activeIndex]" class="text-action">
                <button v-if="list[activeIndex].action">{{ list[activeIndex].action.text }}</button>
            </div>
        </div>
        
        <div v-if="list.length" class="nav-container">
            <button class="nav-btn prev-btn" :disabled="!loaded" @click="slidePrevious">&#5130;</button>
            <button class="nav-btn next-btn" :disabled="!loaded" @click="slideNext">&#5125;</button>
        </div>
         
       
    </div>
</template>

<script>
export default {
  name: 'HeroCarousel',
  props: {
    autoPlay: {
        type: Boolean,
        default: false
    }
  },
    data() {
        return {
            list: [
                {
                    image: 'one.jpeg',
                    title: 'Neque porro',
                    text: 'Neque porro quisquam est qui dolorem ipsum',
                    action: {
                        text: 'Explore'
                    }
                },
                {
                    image: 'two.jpeg',
                    title: 'Sed enim ut sem viverra',
                    text: 'Non odio euismod lacinia at quis. Risus quis varius quam quisque id.',
                    action: {
                        text: 'Check it out'
                    }
                },
                {
                    image: 'three.jpeg',
                    title: 'Id venenatis a condimentum',
                    text: 'Id venenatis a condimentum vitae sapien. Id volutpat lacus laoreet non curabitur. Scelerisque eu ultrices vitae auctor eu augue ut lectus arcu.',
                    action: {
                        text: 'See More'
                    }
                },
                {
                    image: 'four.jpg',
                    title: 'Sit amet justo donec',
                    text: 'Sit amet justo donec enim diam vulputate. Libero id faucibus nisl tincidunt. Tempor commodo ullamcorper a lacus vestibulum. Aliquet bibendum enim facilisis gravida.',
                    action: {
                        text: 'Order Now'
                    }
                },
                {
                    image: 'four.jpg',
                    title: 'Sit amet justo donec',
                    text: 'Sit amet justo donec enim diam vulputate.',
                    action: {
                        text: 'See More'
                    }
                }
            ],
            activeIndex: null,
            isNext: null,
            loaded: true,
            runAnimation: false
        }
    },
    computed: {
        previousIndex() {
            return this.activeIndex <= 0 ? this.list.length - 1 : this.activeIndex - 1
        },
        nextIndex() {
            return this.activeIndex >= this.list.length - 1 ? 0 : this.activeIndex + 1
        }
    },
    mounted() {
        if (this.list.length) {
            this.activeIndex = 0
        }

        if (this.autoPlay) {
            setInterval(() => {
                this.slideNext()
            }, 7000)
        }
    },
  methods: {
    slidePrevious() {
        this.loaded = false
        this.activeIndex = this.activeIndex - 1
        this.isNext = false
        if (this.activeIndex < 0) this.activeIndex = this.list.length - 1
        this.runAnimation = true
         
        setTimeout(() => {
            this.runAnimation = false
            this.isNext = null
            this.loaded = true
        }, 1900);
    },
    slideNext() {
        this.loaded = false
        this.activeIndex = this.activeIndex + 1
        this.isNext = true
        if (this.activeIndex >= this.list.length) this.activeIndex = 0
        this.runAnimation = true

        setTimeout(() => {
            this.runAnimation = false
            this.isNext = null
            this.loaded = true
        }, 1900);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.hero-carousel {
    position: relative;
    width: 100%;
    height: 600px;
    margin: auto;
    transition: 0.5s ease-in-out;
}

@media (min-width: 960px) { .hero-carousel { height: 500px; } }
@media (min-width: 1264px) { .hero-carousel { height: 800px; } }
@media (min-width: 1904px) { .hero-carousel { height: 800px; } }

.slide-container {
    position: relative;
    width: 100%;
    height: 100%;
    overflow: hidden;
}

.animation-wrap, .static-wrap {
    position: absolute;
    top: 0%;
    left: 0%;
    width: 100%;
    height: 100%;
    overflow: hidden;
    background-color: black;
}

.slide {
    width: 100%;
    height: 100%;
    position: absolute;
    background-size: cover;
    background-position: top center;
    border: solid 1px black;
}

.previous {
    top: 15%;
    left: -60%;
    width: 70%;
    height: 70%;
}

.current {
    top: 15%;
    left: 15%;
    width: 70%;
    height: 70%;
}

.next {
    top: 15%;
    left: 90%;
    width: 70%;
    height: 70%;
}

.nextOne { animation: nextOne 2s forwards; }
.nextTwo { animation: nextTwo 2s forwards; }
.nextThree { animation: nextThree 2s forwards; }

.previousOne { animation: previousOne 2s forwards; }
.previousTwo { animation: previousTwo 2s forwards; }
.previousThree { animation: previousThree 2s forwards; }

@keyframes nextOne {
    0% {
        top: 15%;
        left: -60%;
        width: 70%;
        height: 70%;
    }
    33% {
        top: 15%;
        left: -60%;
        width: 70%;
        height: 70%;
    }
    66% {
        top: 15%;
        left: -170%;
        width: 70%;
        height: 70%;
    }
    100% {
        top: 15%;
        left: -170%;
        width: 70%;
        height: 70%;
    }
}

@keyframes nextTwo {
    0% {
        top: 0%;
        left: 0%;
        width: 100%;
        height: 100%;
    }
    33% {
        top: 15%;
        left: 15%;
        width: 70%;
        height: 70%;
    }
    66% {
        top: 15%;
        left: -80%;
        width: 70%;
        height: 70%;
    }
    100% {
        top: 15%;
        left: -80%;
        width: 70%;
        height: 70%;
    }
}

@keyframes nextThree {
    0% {
        top: 15%;
        left: 90%;
        width: 70%;
        height: 70%;
    }
    33% {
        top: 15%;
        left: 90%;
        width: 70%;
        height: 70%;
    }
    66% {
        top: 15%;
        left: 15%;
        width: 70%;
        height: 70%;
    }
    90% {
        top: 0%;
        left: 0%;
        width: 100%;
        height: 100%;
    }
    100% {
        top: 0%;
        left: 0%;
        width: 100%;
        height: 100%;
    }
}

@keyframes previousOne {
    0% {
        top: 15%;
        left: -60%;
        width: 70%;
        height: 70%;
    }
    33% {
        top: 15%;
        left: -60%;
        width: 70%;
        height: 70%;
    }
    66% {
        top: 15%;
        left: 15%;
        width: 70%;
        height: 70%;
    }
    90% {
        top: 0%;
        left: 0%;
        width: 100%;
        height: 100%;
    }
    100% {
        top: 0%;
        left: 0%;
        width: 100%;
        height: 100%;
    }
}

@keyframes previousTwo {
    0% {
        top: 0%;
        left: 0%;
        width: 100%;
        height: 100%;
    }
    33% {
        top: 15%;
        left: 15%;
        width: 70%;
        height: 70%;
    }
    66% {
        top: 15%;
        left: 100%;
        width: 70%;
        height: 70%;
    }
    100% {
        top: 15%;
        left: 100%;
        width: 70%;
        height: 70%;
    }
}

@keyframes previousThree {
    0% {
        top: 15%;
        left: 90%;
        width: 70%;
        height: 70%;
    }
    33% {
        top: 15%;
        left: 90%;
        width: 70%;
        height: 70%;
    }
    66% {
        top: 15%;
        left: 170%;
        width: 70%;
        height: 70%;
    }
    100% {
        top: 15%;
        left: 170%;
        width: 70%;
        height: 70%;
    }
}

.text-container {
    position: absolute;
    height: auto;
    width: 70%;
    top: 40%;
    left: 15%;
    text-align: left;
    font-family: 'Belleza', sans-serif;
}

.text-container .text-title, .text-container .text-description {
    overflow: hidden;
    background: rgba(0, 0, 0, 0.8);
    color: white;
    display: inline-block;
    overflow: hidden;
}

.text-container .text-title h2 {
    padding: 20px;
    padding-bottom: 5px;
    margin: 0;
    animation: titleShow 0.5s;
    font-size: 40px;
    font-family: 'Belleza', sans-serif;
}

.text-container .text-description { 
    animation: descriptionShow 0.5s 0.5 forwards; 
    opacity: 0;
    margin-top: -4px;
}

.text-container .text-description p {
    border-top: solid 3px white;
    padding: 20px;
    margin: 0;
    font-size: 20px;
    font-family: 'Belleza', sans-serif;
}

.text-container button {
    color: white;
    background: #d35400;
    margin-top: 20px;
    border: none;
    border-radius: 50px;
    padding: 20px 60px;
    font-size: 30px;
    font-family: 'Belleza', sans-serif;
    animation: descriptionShow 0.5s 1s forwards; 
    opacity: 0;
}

@keyframes titleShow {
    0% { margin-left: -200px; }
    100% { margin-left: 0px; }
}

@keyframes descriptionShow {
    0% { opacity: 0; }
    100% { opacity: 1; }
}

@keyframes descriptionShow {
    0% { opacity: 0; }
    100% { opacity: 1; }
}

.nav-container {
    position: relative;
    width: 100%;
    pointer-events: none;
}

.nav-container .nav-btn {
    color: white;
    border: none;
    border-radius: 60px;
    background: rgba(0, 0, 0, 0.8);
    font-size: 30px;
    height: 60px;
    width: 60px;
    cursor: pointer;
    bottom: 20px;
}

.nav-container .prev-btn {
    position: absolute;
    left: 20px;
    pointer-events: initial;
}

.nav-container .next-btn {
    position: absolute;
    right: 20px;
    pointer-events: initial;
}
</style>
