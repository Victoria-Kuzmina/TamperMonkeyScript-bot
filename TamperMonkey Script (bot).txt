
// ==UserScript==
// @name         New Userscript
// @namespace    http://tampermonkey.net/
// @version      0.1
// @description  try to take over the world!
// @author       You
// @match        https://yandex.ru/*
// @match        https://xn----7sbab5aqcbiddtdj1e1g.xn--p1ai/*
// @grant        none
// ==/UserScript==
let yandexInput=document.getElementsByName("text")[0];
let searchWords= ["Гобой","Флейта","Саксофон","Валторна","Кларнет","Фагот"];
let searchWord=searchWords[getRandom(0,searchWords.length)];
let i = 0;
if(document.getElementsByClassName("button")[1] !=undefined){
    let timerID = setInterval(()=>{
    yandexInput.value+=searchWord[i];
    i++;
    if(i==searchWord.length) {
        clearInterval(timerID);
        document.getElementsByClassName("button")[1].click();
    }
  }, getRandom(50,1000));
}

else if (location.host == "yandex.ru"){
    let flag = true;
    let links = document.links;
    for (let i=0; i<links.length; i++){
        if (links[i].href.indexOf('xn----7sbab5aqcbiddtdj1e1g.xn--p1ai') != -1){

            links[i].click();
            break;
        }
    }
}
else {
    let links = document.links;
    setInterval(()=>{
        let index = getRandom(0,links.length);
        console.log(links[index]);
        links[index].click();
    },getRandom(1000, 8000));
}

function getRandom(min,max){
    return Math.floor(Math.random()*(max-min)+min);
}

