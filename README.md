# tricks-tricks
boosting tricks
<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<title>TRICKS TRICKS</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<style>
    body {
        font-family: "Trebuchet MS", sans-serif;
        margin: 0;
        padding: 0;
        height: 100vh;
        display: flex;
        justify-content: center;
        align-items: center;
        background: #111;
        color: #fff;
        flex-direction: column;
        overflow: hidden;
    }

    h1 {
        color: #ff4c00;
        margin-bottom: 20px;
        text-align: center;
        margin-top: 60px; /* descendre le titre pour bouton retour */
    }

    /* Page d’intro */
    #controls {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        height: 100vh;
        margin-top: -5vh; /* remonter légèrement */
    }

    select, button {
        font-family: "Trebuchet MS", sans-serif;
        font-size: 22px;
        padding: 15px 20px;
        margin: 10px;
        border-radius: 12px;
        border: none;
        cursor: pointer;
    }

    #youpiBtn {
        background: #ff4c00;
        color: #fff;
        width: 200px;
        text-align: center;
    }

    /* Page tricks */
    #outputContainer {
        display: none;
        justify-content: flex-start; 
        align-items: center;
        flex-direction: column;
        height: 90vh;
        width: 100%;
        position: relative;
        margin-top: 5vh; /* descendre légèrement */
    }

    #output {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: flex-start;
        text-align: center;
        width: 100%;
    }

    .element {
        margin: 5px 0;
        font-size: 26px;
        opacity: 0;
        transform: translateY(20px);
        text-align: center;
        transition: all 0.5s ease;
    }

    .element.show {
        opacity: 1;
        transform: translateY(0);
    }

    #final {
        font-size: 28px;
        text-align: center;
        margin-top: 60px; /* plus bas */
        text-transform: uppercase;
        color: #fff;
        text-shadow: 0 0 5px #fff, 0 0 10px #fff, 0 0 15px #ff4c00, 0 0 20px #ff4c00;
        animation: blinkGlow 1s infinite alternate;
    }

    @keyframes blinkGlow {
        0% {
            opacity: 0.7;
            text-shadow: 0 0 5px #fff, 0 0 10px #fff, 0 0 15px #ff4c00, 0 0 20px #ff4c00;
        }
        50% {
            opacity: 1;
            text-shadow: 0 0 10px #fff, 0 0 20px #fff, 0 0 25px #ff4c00, 0 0 30px #ff4c00;
        }
        100% {
            opacity: 0.8;
            text-shadow: 0 0 5px #fff, 0 0 10px #fff, 0 0 15px #ff4c00, 0 0 20px #ff4c00;
        }
    }

    /* Bouton retour style croix rond liquid glass */
    #backBtn {
        position: fixed;
        top: 20px;
        left: 20px;
        width: 40px;
        height: 40px;
        border-radius: 50%;
        border: none;
        background: rgba(255,255,255,0.1);
        backdrop-filter: blur(8px);
        -webkit-backdrop-filter: blur(8px);
        color: #fff;
        font-size: 24px;
        font-weight: bold;
        display: flex;
        justify-content: center;
        align-items: center;
        cursor: pointer;
        box-shadow: 0 4px 30px rgba(255,255,255,0.1);
        transition: all 0.3s ease;
        z-index: 999;
    }

    #backBtn:hover {
        background: rgba(255,255,255,0.25);
        box-shadow: 0 4px 30px rgba(255,255,255,0.3);
        transform: scale(1.1);
    }
</style>
</head>
<body>
<h1>TRICKS TRICKS</h1>

<div id="controls">
    <label for="niveau" style="font-size:20px; color:#fff;">Choisis ton niveau :</label>
    <select id="niveau">
        <option value="facile">Facile</option>
        <option value="moyen">Moyen</option>
        <option value="difficile">Difficile</option>
        <option value="pro">Pro</option>
    </select>
    <button id="youpiBtn">Youpi !</button>
</div>

<div id="outputContainer">
    <button id="backBtn">&times;</button>
    <div id="output"></div>
    <div id="final"></div>
</div>

<audio id="popSound" src="https://www.soundjay.com/buttons/sounds/button-16.mp3" preload="auto"></audio>

<script>
function getRandomColor() {
    const colors = ["#FF4C00","#00FFFF","#FFCC00","#FF00FF","#00FF00","#FF4444","#00FFCC","#FF9900"];
    return colors[Math.floor(Math.random() * colors.length)];
}

function generateFreestyle(level) {
    const bords = ["forward", "unnatural", "switch", "switch unnatural"];
    let bord = bords[Math.floor(Math.random() * bords.length)];

    const maxRot = { "facile": 540, "moyen": 900, "difficile": 1260, "pro": 1620 };
    let rotations = [];
    for(let r=180; r<=maxRot[level]; r+=180){ rotations.push(r); }
    let rotation = rotations[Math.floor(Math.random()*rotations.length)];

    let typeOptions;
    if(rotation < 720) typeOptions = ["simple"];
    else if(rotation < 1080) typeOptions = ["simple","double"];
    else {
        const allTypes = { "facile": ["simple"], "moyen": ["simple"], "difficile": ["simple","double"], "pro": ["simple","double","triple"] };
        typeOptions = allTypes[level];
    }
    let type = typeOptions[Math.floor(Math.random()*typeOptions.length)];

    let styles = ["cork", "rodeo", "bio", "flat"];
    let style = "";
    if(rotation > 360){
        while(true) {
            style = styles[Math.floor(Math.random() * styles.length)];
            if((style === "rodeo" || style === "flat") && (bord === "switch" || bord === "switch unnatural")) continue;
            break;
        }
    }

    const grabs = ["mute","japan","safety","tail","nose","critical","seatbelt","indy truck","truck driver","handmute","cuban","esco","same nose","high safety","breby",
                  "double mute","double japan","double tail","double nose","double seatbelt","double critical","tindy"];
    let grab;
    while(true) {
        grab = grabs[Math.floor(Math.random()*grabs.length)];
        if(["truck driver","double nose"].includes(grab)) break;
        else break;
    }

    const leadPossible = !["truck driver","double nose"].includes(grab) && Math.random()<0.5;
    let grabDisplay = leadPossible ? "lead "+grab : grab;

    let bonus = "";
    if(grab.includes("safety")) bonus = "safety holding";

    const shiftyOptions = ["shifty","over shifty","double shifty"];
    if(level === "facile" && Math.random()<0.3) grabDisplay = Math.random()<0.5?"shifty":"over shifty";
    if(level !== "facile" && Math.random()<0.3) bonus += (bonus?" + ":"") + shiftyOptions[Math.floor(Math.random()*shiftyOptions.length)];

    let elements = [
        bord !== "forward" ? {label: "Bord", text: bord} : null,
        type !== "simple" ? {label: "Type", text: type+" "+style} : null,
        {label: "Rotation", text: rotation+"°"},
        {label: "Grab", text: grabDisplay},
        bonus ? {label: "Bonus", text: bonus} : null
    ].filter(e => e);

    let typeDisplay = type==="simple"?"":type+" ";
    let finalLine = `${bord !== "forward" ? bord+" " : ""}${typeDisplay}${style} ${rotation} ${grabDisplay}`.replace(/\s+/g,' ').trim();
    if(bonus) finalLine += ` + ${bonus}`; // inclure le bonus

    return { elements, finalLine };
}

const youpiBtn = document.getElementById("youpiBtn");
const backBtn = document.getElementById("backBtn");
const controls = document.getElementById("controls");
const outputContainer = document.getElementById("outputContainer");
const outputDiv = document.getElementById("output");
const finalDiv = document.getElementById("final");
const popSound = document.getElementById("popSound");

youpiBtn.addEventListener("click", ()=>{
    let level = document.getElementById("niveau").value;
    controls.style.display = "none";
    outputContainer.style.display = "flex";
    outputDiv.innerHTML = "";
    finalDiv.innerHTML = "";

    const result = generateFreestyle(level);
    result.elements.forEach((el, idx) => {
        setTimeout(()=>{
            const span = document.createElement("div");
            span.className = `element`;
            span.innerText = `${el.label} : ${el.text}`;
            span.style.color = getRandomColor();
            outputDiv.appendChild(span);

            setTimeout(()=>{ span.classList.add("show"); }, 50);

            popSound.currentTime = 0;
            popSound.play();
        }, idx * 500);
    });

    setTimeout(()=>{
        finalDiv.innerText = result.finalLine;
        popSound.currentTime = 0;
        popSound.play();
    }, result.elements.length * 500 + 300);
});

backBtn.addEventListener("click", ()=>{
    outputContainer.style.display = "none";
    controls.style.display = "flex";
});
</script>
</body>
</html>
