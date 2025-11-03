<script>
let image = [
    "https://www.shutterstock.com/image-photo/these-some-random-photos-260nw-2402066699.jpg",
    "https://miro.medium.com/v2/resize:fit:1400/0*YeaUsQyhXSL1TCTH.png",
    "https://i.redd.it/vd9dc7wfk9471.png"
]
</script>

<main>
    <h1>Denna sida innehåller <strong>fina</strong> bilder</h1>
    <div class="photos">
        <div class="imgwrapper">
            <img src={image[0]} alt="a">
        </div>
        <div class="imgwrapper">
            <img src={image[0]} alt="a">
        </div>
        <div class="imgwrapper">
            <img src={image[2]} alt="a">
        </div>
        <div class="imgwrapper">
            <img src={image[1]} alt="a">
        </div>
        <div class="imgwrapper">
            <img src={image[2]} alt="a">
        </div>
    </div>
</main>

<style>
.imgwrapper {
    flex-grow: 1;
    margin: 10px;
    transition: all 0.2s;
}

.imgwrapper:hover {
    flex-grow: 2;
}

.imgwrapper:active {
    transform: scale(0.9);
}

.imgwrapper img {
    min-width: 300px;
    min-height: 300px;
    width: 100%;
    border-radius: 20px;
    border: 2px dashed #b4befe;
    box-shadow: 4px 8px 0px rgba(0,0,0,0.2);
}

.photos {
    max-width: 90vw;
    margin: auto;
    display: flex;
    flex-wrap: wrap;
    align-items: center;
    justify-content: center;
}

h1 {
    margin: 20px;
    color: #74c7ec;
    font-family: courier;
    display: auto;
    text-align: center;
    font-size: 3em;
    font-weight: bolder;
    background-color: #11111b;
    border-radius: 20px;
    text-shadow:4px 8px 0px rgba(0,0,0,0.2);
}
</style>
