<script>
    let color = "black"

</script>

<main>
    <div class="bg2"></div>
    <div class="container">
        <h1>Registrering</h1>
        <form class="formulär">
            <label for="name">Namn</label>
            <input type="text" id="name" >
            <br>
            <label for="birth">Födelsedatum</label>
            <input type="date" id="birth" >
            <br>
            <label for="email">E-Mail</label>
            <input type="email" id="email" >
            <br>
            <label for="pass">Lösenord</label>
            <input type="password" id="pass" >
            <br>
            <label for="col">Favoritfärg</label>
            <select id="col" bind:value={color}>
                <option value="blue">Blå</option>
                <option value="red">Röd</option>
                <option value="green">Grön</option>
                <option value="black">Svart</option>
                <option value="white">Vit</option>
                <option value="purple">Lila</option>
                <option value="pink">Rosa</option>
                <option value="yellow">Gul</option>
            </select>
<div style="width: 80%; height: 20px; border-radius: 16px; overflow:hidden; background-color:{color}; margin-left: auto; margin-right: auto; margin-top: -17px; z-index:0;">    </div>
<p></p>
<input type="submit" value="Registrera" style="font-family: courier;">
        </form>
    </div>
</main>

<style>
main {
    width: 100%;
    height: 100%;
}

.bg2 {
    display: inline;
    top: 0;
    left: 0;
    background-image: url("https://t4.ftcdn.net/jpg/05/21/65/59/360_F_521655929_N80d5GaCQJ2VP073PfTXJTe9mkvsNtHE.jpg");
    background-size: cover;
    position: fixed;
    z-index: -9;
    opacity: .1;
    width: 100%;
    height: 100%;
    animation: loop 20s infinite;
}

.container {
    border: solid 5px #74c7ec;
    border-radius: 10px;
    width: 35%;
    min-width: 370px;
    height: 70%;
    min-height: 410px;
    background-color: #1e1e2e;
    margin: auto;
    margin-top: auto;
    margin-bottom: auto;
    display: flex;
    flex-direction: column;
    justify-content: space-evenly;
    align-content: center;
}

label {
    font-weight: bold;
}

.formulär {
    display: flex;
    flex-direction: column;
    justify-content: space-evenly;
    align-content: center;

    width: auto;
    height: auto;

    color: #74c7ec;
    font-family: courier;
    text-align: center;
    z-index: 2;
}

input {
    background-color: #313244;
    color: #b4befe;
    width: 80%;
    margin-left: auto;
    margin-right: auto;
    text-align: center;
    border-radius: 16px;
    z-index: 2;
}

#col {
    font-family: courier;
    color: #b4befe;
    
    background-color: #313244;
    width: 80%;
    margin-left: auto;
    margin-right: auto;
    text-align: center;
    border-radius: 16px;
    z-index: 2;
}

h1 {
    color: #74c7ec;
    margin-left: auto;
    margin-right: auto;
}

h1,
h2,
h3,
p {
    font-family: courier;
}

@keyframes loop {
    0% {
        opacity: 0.1;
    }

    50% {
        opacity: 0;
    }

    100% {
        opacity: 0.1;
    }
}
</style>
