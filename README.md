// ==UserScript==
// @name         Yandex bot
// @namespace    http://tampermonkey.net/
// @version      0.1
// @description  try to take over the world!
// @author       Ivan
// @match        https://yandex.ru
// @icon         data:image/gif;base64,R0lGODlhAQABAAAAACH5BAEKAAEALAAAAAABAAEAAAICTAEAOw==
// @grant        none
// ==/UserScript==
let keywords = ["купля-продажа авто", "каталог автомобилей", "автомобили купить"];
let keyword = keywords[getRandom(0, keywords.length)];
let text = document.getElementById('text');
text.value = keyword;
let links = document.links;

if( document.getElementsByClassName("button mini-suggest__button button_theme_search button_size_search i-bem button_js_inited button_hovered_yes").value !== undefined) {
    document.getElementsById("text")[0].value = keyword;
    document.getElementsByClassName("button mini-suggest__button button_theme_search button_size_search i-bem button_js_inited button_hovered_yes")[0].click();

} else {
  for (let i = 0; i < links.length; i++) {
    if (links[i].href.indexOf("auto.ru") !== -1) {
      let link = links[i];
      console.log("Нашел строку " + links[i]);
      links[i].removeAttribute('target');
      link.click();
      break;
    }
  }
}

function getRandom(min, max) {
return Math.floor(Math.random() * (max - min) + min);
}
