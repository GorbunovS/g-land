<template>
    <div class="aboutMe"> 
        <div class="aboutContent">
            <img class="image" src="@/assets/image.png">
            <div class="textContainer">
                <div class="h1">Hello, My name is Stanislav!</div>
                <div class="h2" id="animatedText">
                    I’m professional graffical desigher and frontend developer. Look at my works 
                </div>
                <button class="goBtn">GO!</button>
            </div>
        </div>
    </div>
</template>
<script>
document.addEventListener("DOMContentLoaded", function() {
    const textElement = document.getElementById('animatedText');
    const words = textElement.textContent.split(' ');
    textElement.textContent = ''; 

    words.forEach((word, index) => {
        const span = document.createElement('span');
        span.textContent = word;
        span.style.animation = `appear 1s ease forwards ${index * (5 / words.length)}s`;
        textElement.appendChild(span);  
        if (index < words.length - 1) {
            textElement.appendChild(document.createTextNode(' '));
        }
    });
});
</script>

<style>
@keyframes appear {
    0% {
        opacity: 0;
        transform: translateZ(-50px);
        filter: blur(5px);
    }
    100% {
        opacity: 1;
        transform: translateZ(0);
        filter: blur(0);
    }
}

.aboutMe {
    display: inline-flex;
    flex-direction: column;
    justify-content: flex-end;
    align-items: flex-end;
}
.aboutContent {
    display: flex;
    padding: 0px 9px;
    align-items: center;
    gap: 15px;
}
.textContainer {
    display: flex;
    width: 335px;
    flex-direction: column;
    align-items: flex-start;
    gap: 9px;
}
.h1 {
    color: #FFF;
    text-align: center;
    font-family: "TT Runs Trial";
    font-size: 17px;
    font-style: normal;
    font-weight: 500;
    line-height: normal;
}
.h2 {
    color: #FFF;
    font-family: "TT Runs Trial";
    font-size: 15px;
    font-style: normal;
    font-weight: 300;
    line-height: normal;
}
.h2 span {
    opacity: 0;
    display: inline-block;
}
.goBtn {
    font-family: "TT Runs Trial";
    color: #FFF;
    padding: 0px 12px 0px 13px;
    justify-content: center;
    align-items: center;
    background: rgba(113, 113, 113, 0.50);
    align-self: flex-end; /* This will align the button to the right within its container */
}
.goBtn:hover {
    background: rgba(205, 205, 205, 0.50);
}
</style>
