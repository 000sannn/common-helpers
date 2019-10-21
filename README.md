#GET RANDOM ELEMENT IN LIST BY PRE FIXED RATE
```
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
