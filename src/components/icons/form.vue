<template>
    <!-- Vue component template -->
    <form>
        <!-- Form to display and interact with facilities -->
        <h1>Facilities</h1>
        <!-- Title of the form -->

        <ul>
            <!-- Loop through the facilities array to list items -->
            <li 
                v-for="facility in facilities" 
                v-on:click="toggleActive(facility)" 
                v-bind:class="{ 'active': facility.active }">
                <!-- Display facility name and price -->
                {{ facility.name }} <span>{{ formatCurrency(facility.price) }}</span>
            </li>
        </ul>

        <div class="total">
            <!-- Display the calculated total price -->
            Total: <span>{{ formatCurrency(total()) }}</span>
            <!-- Show the total price with proper formatting -->
        </div>
    </form>
</template>

<script>
export default {
    // Component export to be used in Vue applications
    data() {
        // Define the reactive state of the component
        return {
            facilities: [
                {
                    name: 'Ballroom',
                    price: 5000,
                    active: true
                },{
                    name: 'Backyard',
                    price: 400,
                    active: false
                },{
                    name: 'Wellness Area',
                    price: 250,
                    active: false
                },{
                    name: 'Restaurant',
                    price: 220,
                    active: false
                }
            ]
        }
    },
     methods: {
        // This method toggles the "active" state of a facility when clicked
        toggleActive(facility) {
            facility.active = !facility.active; // Flip the active status
        },
        // Method to calculate the total price of all active facilities
        total() {
            let total = 0;   // Initialize total as 0
            // Iterate through each facility in the facilities array
            this.facilities.forEach(facility => { 
                if (facility.active) { // Check if the facility is active
                    total += facility.price; // Add the price to the total
                }
            });
            return total; // Return the calculated total
        },
        // Method to format a number as currency (e.g., $5000.00)
        formatCurrency(value) {
            return `$${value.toFixed(2)}`; // Add a dollar sign and ensure two decimal places
        }
    }
  }
</script>

<style scoped>
  /* Scoped CSS styles */
  form {
    /* Styling for the form */
    background-color: #8931EF;
    border-radius: 2px;
    box-shadow: 0 1px 1px #ccc;
    width: 400px;
    padding: 35px 60px;
    margin: 50px auto;
  }

  h1 {
    /* Styling for heading */
    color: #fff;
    font-size: 64px;
    font-family: 'Cookie', cursive;
    font-weight: normal;
    line-height: 1;
    text-shadow: 0 3px 0 rgba(0, 0, 0, 0.1);
  }

  ul {
    /* Styling for unordered list */
    list-style: none;
    color: #fff;
    font-size: 20px;
    font-weight: bold;
    text-align: left;
    margin: 20px 0 15px;
  }

  li {
    /* Styling for list item */
    padding: 20px 30px;
    background-color: #a5949a;
    margin-bottom: 8px;
    box-shadow: 0 1px 1px rgba(0, 0, 0, 0.1);
    cursor: pointer;
  }

  li.active {
    /* Styling for active list item */
    background-color: #87E911;
  }

  .total {
    /* Styling for total */
    border-top: 1px solid rgba(255, 255, 255, 0.5);
    padding: 15px 30px;
    font-size: 20px;
    font-weight: bold;
    text-align: left;
    color: #fff;
  }

  .total span {
    /* Styling for total span */
    float: right;
  }
  </style>
