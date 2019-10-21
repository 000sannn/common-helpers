## GET RANDOM ELEMENT IN LIST BY PRE FIXED RATE
```javascript
/**
 * return a random element in list by it own rate
 * @param {object} list 
 * 
 * list is a array of element by format {value: any, rate: 0 -> 1}
 */
function randomByRatio(list) {
    const randomPick = Math.random();
    const avg = list.map(i => i.rate).reduce((acc, curr) => acc + curr)

    let holder = randomPick;

    const pickList = list.map(i => ({ ...i, rate: i.rate / avg }));

    for (const i in list) {
        holder = holder - pickList[i].rate;
        if (holder <= 0) {
            list[i].pickRate = pickList[i].rate;
            if (!list[i].pickCount) { list[i].pickCount = 0 };
            list[i].pickCount++
            return list[i];
        }
    }

    return list[Math.floor(Math.random() * list.length)];
}
```

## RETURN DATE BY DEFINED FORMAT
```javascript
const formatDateTime = (rawDate, format = 'mm-dd-yyyy h:m') => {
    let date = new Date();

    if (rawDate) {
        try {
            const timestamp = Number(rawDate);
            const time = isNaN(timestamp) ? rawDate : timestamp;
            date = new Date(time);
        } catch (e) {
            date = new Date(rawDate);
        }
    }


    const months = date.getMonth() + 1;
    const days = date.getDate();
    const years = date.getFullYear();
    const hours = date.getHours();
    const minutes = date.getMinutes();
    const seconds = date.getSeconds();

    const mm = months < 10 ? "0" + months : months;
    const dd = days < 10 ? "0" + days : days;
    const yyyy = years;

    const h = hours < 10 ? "0" + hours : hours;
    const m = minutes < 10 ? "0" + minutes : minutes;
    const s = seconds < 10 ? "0" + minutes : seconds;

    const formatedTime = { mm, dd, yyyy, h, m, s };
    for (const timeUnit in formatedTime) {
        format = format.replace(timeUnit, formatedTime[timeUnit]);
    }

    return format;
}

```
