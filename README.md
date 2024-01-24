# notcoin_AutoClicker

Very simple, no need for web telegram

  1. Need Enable webview inspecting option (in the `Telegram settings => Advanced => Experimental settings => Enable webview inspecting`)
  2. Press **F12** then in the console tab
  3. Type the text below

## To bypass Telegram desktop mode "Desktop is boring."

```
function changeURL() {
    function getParameterByName(name, url) {
        if (!url) url = window.location.href;
        name = name.replace(/[\[\]]/g, '\\$&');
        var regex = new RegExp('[?&]' + name + '(=([^&#]*)|&|#|$)'),
            results = regex.exec(url);
        if (!results) return null;
        if (!results[2]) return '';
        return decodeURIComponent(results[2].replace(/\+/g, ' '));
    }

    function isTargetSite(url) {
        return url.includes('https://clicker.joincommunity.xyz/clicker');
    }
    let currentPlatform = getParameterByName('tgWebAppPlatform');
    if (currentPlatform === 'tdesktop' && isTargetSite(window.location.href)) {
        let newURL = window.location.href.replace('tgWebAppPlatform=tdesktop', 'tgWebAppPlatform=ios');
        window.location.href = newURL;
        window.location.reload();
    }
}
changeURL();
```

### Run Autoclicker (+ click on rocket)

```
function autoClicker() {
    let powerLimitForAutotap = 100;
    let countclicks = 34;
    let recharging = false;
    let skipClick = false;

    let app_root = document.querySelector('div[class^="_root"]');
    let multipleClicks = 45;
    if (multipleClicks === undefined || multipleClicks === null) { multipleClicks = 0; }

    async function click() {
        let cc = document.querySelectorAll('div[class^="_notcoin"]');
        let scoreElement = document.querySelector('div[class^="_scoreCurrent"]');
        let score = parseInt(scoreElement.textContent);

        try {
            let imrocket = document.querySelectorAll('img[class^="_root"]');
            imrocket[0][Object.keys(imrocket[0])[1]].onClick();
            recharging = false;
        } catch (error) {}

        for (let step = 0; step < countclicks; step++) {
            score = parseInt(scoreElement.textContent);

            if (skipClick) {
                break;
            }

            if (recharging) {
                if (score >= powerLimitForAutotap) {
                    recharging = false;
                }
                break;
            }

            if (score > multipleClicks * 2) {
                try {
                    await new Promise((resolve) => {
                        cc[0][Object.keys(cc[0])[1]].onTouchStart('');
                        setTimeout(resolve, 100);
                    });
                } catch (error) {}
            } else {
                recharging = true;
                break;
            }
        }
    }

    setInterval(click, 350);
}

autoClicker();

```

---

### How to work?



https://github.com/omidRR/notcoin_AutoClicker/assets/64539596/68450501-b111-4bdf-836b-bd0ab821a4a3


