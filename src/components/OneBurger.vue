<template>
    <div>

        <div class="gallery">
            <div class="firstburger">
                <ul>
                {{burger.name}}
            </ul>


                <img v-bind:src="burger.img" alt="en hamburgare" />
                <button v-on:click = "addBurger">+</button>
                {{amountOrdered}}
                <button v-on:click = "deleteBurger">-</button>


             <!--   <ol>
                    <li> 1 Cheese burger</li>
                    <li>cheese, tomato, cucumber</li>
                    <section class="Gluten">
                        <p>Includes <span id="Gluten">Gluten </span></p>
                    </section>
                </ol>

                <ul>
                    <li>Recomended drinks:</li>
                    <li>IPA</li>
                    <li>Red Ale</li>
                    <li>Imperial Stout</li>
                </ul> -->
            </div>
            <!--      <div class="secondburger">
        Secondburger
        <section>

            <img src="Halloumi.jpg" alt="en hamburgare" />

            <ol>
                <li> 2 Cheese burger</li>
                <li>cheese, tomato, cucumber</li>
                <li>Includes Lactose and Gluten </li>
            </ol>

            <ul>
                <li>Recomended drinks:</li>
                <li>IPA</li>
                <li>Red Ale</li>
                <li>Imperial Stout</li>
            </ul>
        </section>
    </div>
    <div class="thirdburger">

            <img src="chickenburger.jpg" alt="en hamburgare" />

            <ol>
                <li>Cheese burger</li>
                <li>cheese, tomato, cucumber</li>
                <li>Includes Lactose and Gluten </li>
            </ol>

            <ul>
                <li>test Recomended drinks:</li>
                <li>IPA</li>
                <li>Red Ale</li>
                <li>Imperial Stout</li>
            </ul>

    </div> -->

        </div>
        <ul>
         <li>
             {{ burger.name }}
         </li>
         <li>
            {{ burger.kCal }}
         </li>
         <li>
            {{ burger.lactose }}
         </li>
         <li>
            {{ burger.gluten }}
         </li>

        </ul>
         <div>
             <!--   <Burger v-bind:src="hamburgare1.jpg" /> -->
        </div>
        </div>
    </template>

      <script>
      export default {
        name: 'OneBurger',
        props: {
          burger: Object
        },
        data: function () {
            return {
                amountOrdered:0,
            }
        },

    methods:{
            addBurger: function () {
                this.amountOrdered++;
                this.$emit('orderedBurger', { name:   this.burger.name, 
                                amount: this.amountOrdered 
                              }
                )
                
            },
            deleteBurger: function () {
                this.amountOrdered--;
                this.$emit('orderedBurger', { name:   this.burger.name, 
                                amount: this.amountOrdered 
                              }
                )
            }
        }

      }
          



      </script>

      <!-- Add "scoped" attribute to limit CSS to this component only -->
        <style scoped>
        </style>
