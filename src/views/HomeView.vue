<template>
    <div>
        <link href='https://fonts.googleapis.com/css?family=Patrick Hand' rel='stylesheet'>
        <div>
            <div>
                <section class="start">
                    <div class="resturant">
                        <img src="resturant.jpg" alt="en resturang" />
                        <div class="top-left"><h1>Burgers Online</h1></div>
                    </div>
                   <div class="Menuitems">
                    <nav> <h3>Menu items</h3> </nav>
                    </div> 
                </section>
            </div>
            
            <li class="burgarmeny">
                
                <Burger v-for="burger in burgers"
                v-bind:burger="burger"
                v-bind:key="burger.name"
                v-on:orderedBurger="addToOrder($event)" />
            </li>
            
        </div>
        
        <div>
            <main>
                <section id="contact" class="contact">
                    <form>
                        <p>
                            <label for="first last">Full Name</label><br>
                            <input type="text" id="first last" v-model="fln" required="required" placeholder="First and Last">
                        </p>
                        <p>
                            <label for="email">Email</label><br>
                            <input type="email" id="email" v-model="em" required="required" placeholder="E-mail address">
                        </p>
                        
                    </form>
                    
                </section>
            </main>
        </div>
        <div>Selected: {{ payment }}</div>
        
        <select v-model="payment">
            <option disabled value="">Please select payment method</option>
            <option value="Credit card">Credit card</option>
            <option value="Swish">Swish</option>
            <option value="Cash">Cash</option>
        </select>
        
        <div>Checked gender: {{ checkedGender }}</div>
        
        <input type="radio" id="female" value="Female" v-model="checkedGender">
        <label for="female">Female</label>
        
        <input type="radio" id="male" value="Male" v-model="checkedGender">
        <label for="male">Male</label>
        
        <input type="radio" id="no" value="Do no wish to provide" v-model="checkedGender">
        <label for="no">Do not wish to provide</label>
        
        <div id="example-1">
            <button v-on:click="order">Beställ</button> </div>
          <div id= "fitmap"> 
            <div id="map" v-on:click="setLocation" v-bind:style="{ background: 'url(' + require('../../public/img/polacks.jpg')+ ')' }">
                <div v-bind:style="{ left: location.x + 'px', top: location.y + 'px'}">
                    T
                </div>
            </div>
        </div> 
            
            
        </div>
        
        
        
        
    </template>
    
    <script>
    import menu from '../assets/menu.json'
    import Burger from '../components/OneBurger.vue'
    import io from 'socket.io-client'
    
    const socket = io();
    /*  function MenuItem(name, URL, kCal, glutenandlactose) {
        this.burgerName = name;
        this.amountkCal = kCal;
        this.glutenandlactose = glutenandlactose;
        this.URL= URL; 
    }
    // creating objects
    const burger1 = new MenuItem("Burger1", "hamburgare1.jpg", "400", "Gluten and Lactose");
    const burger2 = new MenuItem("Burger2", "Halloumi.jpg", "450", "Gluten and Lactose");
    const burger3 = new MenuItem("Burger3", "chickenburger.jpg", "300", "Gluten and Lactose");
    
    console.log(burger1.burgerName, burger1.amountkCal, burger1.glutenandlactose);
    console.log(burger2.burgerName, burger2.amountkCal, burger2.glutenandlactose);
    console.log(burger3.burgerName, burger3.amountkCal, burger3.glutenandlactose);
    var myArray = [burger1, burger2, burger3]; */
    
    
    
    
    export default {
        name: 'HomeView',
        components: {
            Burger
        },
        
        data: function () {
            return {
                burgers: menu,
                payment: "",
                checkedGender: "", 
                orderedBurgers:{},
                fln: "",
                em: "",
                st: "",
                nr: "",
                location: { x: 0, y: 0 },
                
                
            }
        },
        
        
        
        
        methods: {
            getOrderNumber: function () {
                return Math.floor(Math.random()*100000);
            },
            
            
            setLocation: function (event) {
                var offset = {x: event.currentTarget.getBoundingClientRect().left,
                    y: event.currentTarget.getBoundingClientRect().top};
                    this.location = { x: event.clientX - 10 - offset.x,
                        y: event.clientY - 10 - offset.y };
                        
                    },
                    
                    addToOrder: function (event) {
                        this.orderedBurgers[event.name] = event.amount;
                        console.log(event, this.orderedBurgers);
                    },
                    
                    order: function() {
                        console.log("Din beställning är lagd" + this.checkedGender + this.fln + this.orderedBurgers )
                        socket.emit("addOrder", { orderId: this.getOrderNumber(),
                            details: { x: this.location.x,
                                y: this.location.y, payment: this.payment, checkedGender: this.checkedGender,
                                fln: this.fln, em: this.em, st: this.st, nr: this.nr },
                                orderItems: this.orderedBurgers
                            }
                            ); 
                            
                        },
                        
                        
                        /*addToOrder: function (event) {
                            this.orderedBurgers[event.name] = event.amount;
                            console.log(event, this.orderedBurgers); 
                        } */
                    }
                }
                
                
                
            </script>
            
            <style>
            
            body {
                font-family: "Patrick Hand";
                font-size: 16pt;
                background-color: #FBEAFF;
            }
            
            .Menuitems{
                font-family: "Patrick Hand";
            }
            .resturant {
                width: 1300px;
                height: 300px;
                opacity: 0.8;
            }
            
            .Alternatives {
                background-color: black;
                color: white;
            }
            .Firstburger {
                margin: 1px 20px 20px 1px;
                border: 2px solid #ff9900;
            }
            
            .Secondburger {
                margin: 1px 20px 20px 1px;
                border: 2px solid #ff9900;
            }
            
            .Thirdburger {
                margin: 1px 20px 20px 1px;
                border: 2px solid #ff9900;
            }
            .button:hover {
                background-color: #4CAF50; /* Green */
                color: white;
            }
            .Gluten {
                color: #ff5500;
            }
            
            #Gluten {
                text-transform: uppercase;
            }
            .resturant {
                width: 1300px;
                height: 300px;
                opacity: 0.8;
            }
            
            /* Resize images */
            .resturant img {
                width: 100%;
                height: 300px;
                opacity: 0.8;
            }
            
            .resturant {
                position: relative;
                text-align: center;
                color: black;
            }
            
            .top-left {
                position: absolute;
                top: 1px;
                left: 40px;
                font-size: 3em;
            }
            .gallery {
                display: grid;
                grid-template-columns: auto auto auto;
                grid-gap: 15px;
            }
            .firstburger {
                grid-column: 1;
            }
            .secondburger {
                grid-column: 2;
            }
            .Thirdburger {
                grid-column: 3;
                
            }
            .burgarmeny {
                display: grid;
                grid-gap: 10px;
                grid-template-columns: 33% 33% 33%;
                background-color: #B39CD0;
                font-family: "Patrick Hand";

            }

            #map {
                position: relative;
                margin: 0;
                padding: 0;
                background-repeat: no-repeat;
                width:1920px;
                height: 1078px;
                cursor: crosshair;
                
            }
            #fitmap {
                overflow:scroll;
            }
            
            #map div {
                position: absolute;
                background: black;
                color: white;
                border-radius: 10px;
                width:20px;
                height:20px;
                text-align: center;
            }
            
            
            
            
        </style>