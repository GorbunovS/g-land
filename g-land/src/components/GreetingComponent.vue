<template>
    <div class="aboutMe"> 
        <div class="aboutContent">
        <img class="image" src="@/assets/image.png">
        <div class="textContainer">
            <div class="h1">Hello, My name is Stanislav! 
            </div>
            <div class="h2">
                I’m professional graffical desigher and frontend developer.
Look at my works 
            </div>
        </div>
        
        </div>
    </div>
</template>

<style>
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
/* .goBtn {
    font-family: "TT Runs Trial";
    color: #FFF;
    padding: 0px 12px 0px 13px;
    justify-content: center;
    align-items: center;
    background: rgba(113, 113, 113, 0.50);
}
.goBtn:hover {
    background: rgba(205, 205, 205, 0.50);
} */
</style>