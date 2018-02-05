# Street Fighter V Ranking Twitch Command
### Step-by-step to create a command for Twitch chat that will display the Ranking and League Points for a player.

**REQUIREMENTS**
* [Google Chrome](https://www.google.com.br/chrome/)
* [Tampermonkey](http://tampermonkey.net/) (Extension for Google Chrome)
* [Downloads Overwrite Existing Files](https://chrome.google.com/webstore/detail/downloads-overwrite-exist/fkomnceojfhfkgjgcijfahmgeljomcfk) (Extension for Google Chrome)
* [Streamlabs Chatbot](https://streamlabs.com/chatbot)

## Installation

1. Install Google Chrome and both extensions listed above.

2. Ctrl + C, Ctrl + V the script below on your Tampermonkey.

````javascript
// ==UserScript==
// @name         Street Fighter V Points
// @namespace    http://tampermonkey.net/
// @version      1.0
// @description  Script who gets League Points/Ranking, put in a text file and download.
// @author       Carlos Soler
// @match        https://game.capcom.com/cfn/sfv/profile/*
// @grant        none
// ==/UserScript==

(function() {
    'use strict';

    setInterval(function(){
        location.reload();
    }, 30000);

    $(document).ready(function() {
        var lp = $('.leagueInfo dd:last').text().replace('LP','');
        var wins = $('.win .total:first').text();
        var losses = $('.lose .total:first').text();
        var league;

        if ((lp >= 1) && (lp <= 499)) league = 'Rookie';
        if ((lp >= 500) && (lp <= 999)) league = 'Bronze';
        if ((lp >= 1000) && (lp <= 1499)) league = 'Super Bronze';
        if ((lp >= 1500) && (lp <= 1999)) league = 'Ultra Bronze';
        if ((lp >= 2000) && (lp <= 2999)) league = 'Silver';
        if ((lp >= 3000) && (lp <= 3499)) league = 'Super Silver';
        if ((lp >= 3500) && (lp <= 3999)) league = 'Ultra Silver';
        if ((lp >= 4000) && (lp <= 5499)) league = 'Gold';
        if ((lp >= 5500) && (lp <= 6499)) league = 'Super Gold';
        if ((lp >= 6500) && (lp <= 7499)) league = 'Ultra Gold';
        if ((lp >= 7500) && (lp <= 9999)) league = 'Platinum';
        if ((lp >= 10000) && (lp <= 11999)) league = 'Super Platinum';
        if ((lp >= 12000) && (lp <= 13999)) league = 'Ultra Platinum';
        if ((lp >= 14000) && (lp <= 19999)) league = 'Diamond';
        if ((lp >= 20000) && (lp <= 24999)) league = 'Super Diamond';
        if ((lp >= 25000) && (lp <= 29999)) league = 'Ultra Diamond';
        if ((lp >= 30000) && (lp <= 34999)) league = 'Master';
        if (lp >= 35000) league = 'Grand Master';

        var data = 'Ranking atual: '+lp+'LP ('+league+') - Últimas 20 partidas: '+wins+' vitórias / '+losses+' derrotas';

        var a = document.createElement('a');
        a.href = 'data:application/txt;charset=utf-8,' + encodeURIComponent(data);
        a.download = 'sfv_lp.txt';
        document.getElementsByTagName('body')[0].appendChild(a);
        a.click();
    });
})();
````

3. You will need to access the profile page who you want to show, for example: https://game.capcom.com/cfn/sfv/profile/Batera. Activate the Tempermonkey script, refresh the page and it should start downloading a txt file called "sfv_lp.txt" each 30 seconds.

4. Create the following command on Streamlabs Chatbot:

>Command: !sfv (or whatever you prefer)
>Response: $readline(C:\Users\YOUR_USER\Downloads\sfv_lp.txt)

## Screenshots
![](assets/screenshot-1.png)  
1. 

![](assets/screenshot-2.png)  
2. 

![](assets/screenshot-3.png)  
3. 

![](assets/screenshot-4.png)
4. 