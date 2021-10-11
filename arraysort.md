Here's how you'd return an array of every item in the game in the GCLI (probably don't do this):
```
js Item.all();
```
Here's your array in the GCLI:
```
0 => seal-clubbing club
1 => seal tooth
2 => helmet turtle
...
10627 => French-Transylvanian Dictionary
```

---
Here's how you'd filter out every item in that array you don't have:
```
js Item.all().filter((anItem) => availableAmount(anItem) > 0);
```
Which will return something like:
```
0 => seal tooth
1 => helmet turtle
2 => spices
...
2561 => French-Transylvanian Dictionary
```
Notice how the number of the item numbers on the same items shift between both this example and the previous one. These reflect the item's position in the array you've generated, not the item's cannonical item number.

---
Here's how you'd filter out everything you don't own and everything that isn't a one-handed weapon (look, you can do && inside function calls!):
```
js Item.all().filter((item) => availableAmount(item) > 0 && weaponHands(item) === 1);
```
Which will return something like:
```
0 => seal-clubbing club
1 => turtle totem
2 => pasta spoon
...
128 => industrial fire extinguisher
```
---
Here's how you'd rank your weapons listed in the previous example by familiar weight (this is starting to get long):
```
js Item.all().filter((item) => availableAmount(item) > 0 && weaponHands(item) === 1).sort((a, b) => numericModifier(b, "Familiar Weight") - numericModifier(a, "Familiar Weight"));
```
Which will return something like:
```
0 => cursed pirate cutlass
1 => gnawed-up dog bone
2 => industrial fire extinguisher
...
128 => batblade
```
You might notice that only the first two items actually even provide familiar weight and there's a lot of items in the array that don't - we only sorted the array, we did not filter it again.

---
Here's how you could provide only the five best familiar weight from the previous array:
```
js Item.all().filter((item) => availableAmount(item) > 0 && weaponHands(item) === 1).sort((a, b) => numericModifier(b, "Familiar Weight") - numericModifier(a, "Familiar Weight")).slice(0,5);
```
Which will return something like:
```
0 => cursed pirate cutlass
1 => gnawed-up dog bone
2 => industrial fire extinguisher
3 => seal-clubbing club
4 => saucepan
```