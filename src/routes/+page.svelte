<!--Delar upp sidan i två delar-->
<main>
    <div>

        <h1 class="name"> Ali </h1>
        <br>
        <br>
        <h2>Här har jag samlat mina uppgifter som jag gjort i samband med webbutveckling i årskurs 2 på Maja Beskowgymnasiet!</h2>
        <br>
        <br>
        <br>
        <h3>Inspirerande citat för min webbutvecklingsresa: hej</h3>
        <!--Under denna kommer vi lägga till fler element-->
        <br>
        <br>
        <br>
        <p id="inspo">
            "The only way to learn a new programming language is by writing programs in it." <br>- <strong>Dennis Ritchie</strong>,<sub>creator of the C programming language.</sub><br>
        </p>

        <br>
        <br>
        <div id="quote">
            <p>
                "Every great developer you know got there by solving problems they were unqualified to solve until they actually did it." - <span>Patrick McKenzie, software engineer and entrepreneur</span>.
            </p>
        </div>

    </div>
    <!--Här kommer vi lägga till en bild senare i uppgiften 1.2.4 Extra styling-->
    <svg viewBox="0 0 300 300" xmlns="http://www.w3.org/2000/svg">
        <path fill="#181825" d="M29.5,-44C37.1,-41,41.4,-30.9,43.5,-21.3C45.7,-11.7,45.8,-2.5,46.6,8.2C47.5,19,49.1,31.5,43.9,38.7C38.7,45.9,26.6,47.8,14.3,53.8C1.9,59.9,-10.8,70,-18.4,66.2C-26,62.4,-28.6,44.7,-40.2,33.5C-51.8,22.4,-72.5,17.9,-75.7,9.6C-78.8,1.3,-64.3,-10.7,-56.1,-24.3C-47.8,-37.9,-45.8,-53,-37.5,-55.7C-29.2,-58.3,-14.6,-48.4,-1.8,-45.6C10.9,-42.7,21.9,-46.9,29.5,-44Z" transform=" translate(200,70)"  />
    </svg>

</main>

<style>
main {
    /*Styling för att dela upp sidan i två delar. */
    /*Vi kommer gå igenom detta i detalj senare*/
    margin: auto;
    width: 80vw;
    height: 70vh;
    display: grid;
    grid-template-columns: repeat(2, 50%);
    overflow: hidden;
}

div {
    /*Styling för att centrera texten i behållaren*/
    margin: auto;
}

h1 {
    color: #74c7ec;
}

h2 {
    color: #b4befe;
    margin: auto;
}

h3 {
    color: #cdd6f4;
    font-family: sans-serif;
    font-weight: bold;
}

.name {
    border-radius: 20px;
    border: 10px solid #11111b;
    background-color: #11111b;
    font-size: 50px;
    text-shadow: 0px 0px 4px #74c7ecaa;
}

#inspo {
    font-size: 160%;
    color: #74c7ec;
}

#quote {
    border-radius: 10px;
    background-color: #74c7ec;
}

span {
    color: green;
}

h1,
h2,
h3,
p {
    font-family: courier;
    display: inline;
    /*Ger utrymme mellan element*/
    margin-top: 20px;
}

p sub {
    opacity: 0.5;
    font-size: small;
}

p strong {
    text-shadow: 0px 0px 4px #74c7ec72;
}
</style>
