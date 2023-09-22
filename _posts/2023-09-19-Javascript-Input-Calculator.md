---
title: JS Input Calculator
comments: true
hide: true
layout: post
description: A common way to become familiar with a language is to build a calculator.  This calculator shows off button with actions.
courses: {'compsci': {'week': 5}}
type: hacks
---

<!-- Heading -->
> <h1>Grade Calculator</h1>
> <h2>Input scores, press tab to add each new number.</h2>
<!-- Totals -->
<h3>
    Total : <span id="total">0.0</span>
    Count : <span id="count">0.0</span>
    Average : <span id="average">0.0</span>
</h3>
<!-- Clear button -->
<!-- <button onclick="clearScores()">Clear</button> -->
<!-- Rows -->
<div id="scores">
    <!-- javascript generated inputs -->
</div>
<style>
  /* Style for input elements */
  input[type="number"] {
    background-color: #9ef0ba; /* Change this to the desired background color */
    color: #000000; /* Change this to the desired text color */
    border: 1px solid #000000; /* Change this to the desired border color */
    /* Add other styles as needed */
  }
</style>
<script>
// Creates a new input box
function newInputLine(index) {
    // Add a label for each score element
    var title = document.createElement('label');
    title.htmlFor = index;
    title.innerHTML = index + ". ";
    document.getElementById("scores").appendChild(title); // add to HTML
    // Setup score element and attributes
    var score = document.createElement("input"); // input element
    score.id =  index;  // id of input element
    score.onkeydown = calculator // Each key triggers event (using function as a value)
    score.type = "number"; // Use text type to allow typing multiple characters
    score.name = "score";  // name is used to group "score" elements
    score.style.textAlign = "right";
    score.style.width = "5em";
    document.getElementById("scores").appendChild(score);  // add to HTML
    // Create and add blank line after input box
    var br = document.createElement("br");  // line break element
    document.getElementById("scores").appendChild(br); // add to HTML
    // Set focus on the new input line
    document.getElementById(index).focus();
}
// Handles event and calculates totals
function calculator(event) {
    var key = event.key;
    // Check if the pressed key is the "Tab" key (key code 9) or "Enter" key (key code 13)
    if (key === "Tab" || key === "Enter") {
        event.preventDefault(); // Prevent default behavior (tabbing to the next element)
        var array = document.getElementsByName('score'); // setup array of scores
        var total = 0;  // running total
        var count = 0;  // count of input elements with valid values
        for (var i = 0; i < array.length; i++) {  // iterate through array
            var value = array[i].value;
            if (parseFloat(value)) {
                var parsedValue = parseFloat(value);
                total += parsedValue;  // add to running total
                count++;
            }
        }
        // update totals
        document.getElementById('total').innerHTML = total.toFixed(2); // show two decimals
        document.getElementById('count').innerHTML = count;
        if (count > 0) {
            document.getElementById('average').innerHTML = (total / count).toFixed(2);
        } else {
            document.getElementById('average').innerHTML = "0.0";
        }
        // adds newInputLine, only if all array values satisfy parseFloat
        if (count === document.getElementsByName('score').length) {
            newInputLine(count); // make a new input line
        }
    }
//function clearScores() {
// Remove the first input box and label
    //function clearTable() {
    //var scoresContainer = document.getElementById('scores');
    //scoresContainer.innerHTML = ''; // Remove all existing input lines
    //document.getElementById('total').innerHTML = '0.0';
    //document.getElementById('count').innerHTML = '0.0';
    //document.getElementById('average').innerHTML = '0.0';
    // Creates 1st input box on Window load
       // newInputLine(0);
    //}
}
// Attach the clearScore function to the "Clear" button
//var clearButton = document.getElementById('clearButton');
//clearButton.addEventListener('click', clearScore)
// Creates 1st input box on Window load
newInputLine(0);
</script>