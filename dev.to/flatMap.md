# flatMap() - JavaScript Array method - ES2021

&emsp; Have you ever wondered if there is any simple way to create an array from an existing nested array of objects' property?

&emsp; Consider this example. You have an array of objects that contain the product information

```JavaScript
const productsArray = [
    {name: 'Shirt', variants: [{color: 'red', size: 'S'}, {color: 'blue', size: 'M'}]},
    {name: 'Pants', variants: [{color: 'green', size: 'L'}, {color: 'black', size: 'XL'}]},
    {name: 'Dress', variants: [{color: 'pink', size: 'S'}, {color: 'purple', size: 'M'}]}
];
```

&emsp; So from this example, you need to create an array which has all the `variants` array values. In this case, traditionally, `map()` method might be used.

```JavaScript
const variantsArrays = products.map(product => product.variants);
console.log(variantsArrays);
```

Output will be

```JavaScript
[ [ { color: 'red', size: 'S' }, { color: 'blue', size: 'M' } ],
  [ { color: 'green', size: 'L' }, { color: 'black', size: 'XL' } ],
  [ { color: 'pink', size: 'S' }, { color: 'purple', size: 'M' } ] ]
```
&emsp; If you see this carefully, this is just an array, that is containing the arrays of variants from each object in the `productsArray`.

&emsp; Now, to make this more readable and as a single array of objects, we will apply `flat()` method to the same.

```JavaScript
const allVariants = variantsArrays.flat();
console.log(allVariants);
```
Output will be

```JavaScript
[ { color: 'red', size: 'S' },
  { color: 'blue', size: 'M' },
  { color: 'green', size: 'L' },
  { color: 'black', size: 'XL' },
  { color: 'pink', size: 'S' },
  { color: 'purple', size: 'M' } ]
```

## Issue

&emsp; As you can see, using `map()` and `flat()` separately requires two separate steps, and also the result is the same, but the code is more verbose and harder to read. So, developers had to use nested loops and chaining multiple array methods to flatten and map nested arrays.

## Solution

&emsp; To overcome this issue, `flatMap()` method has been introduced with ES2021 update.

### Definition (from [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/flatMap)) <br /><br />

> The `flatMap()` method returns a new array formed by applying a given callback function to each element of the array, and then flattening the result by one level. It is identical to a `map()` followed by a `flat()` of depth 1 (arr.map(...args).flat()), but slightly more efficient than calling those two methods separately.

## Syntax (from [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/flatMap))
<br /><br />


```JavaScript
// Arrow function
flatMap((element) => { /* … */ })
flatMap((element, index) => { /* … */ })
flatMap((element, index, array) => { /* … */ })

// Callback function
flatMap(callbackFn)
flatMap(callbackFn, thisArg)

// Inline callback function
flatMap(function (element) { /* … */ })
flatMap(function (element, index) { /* … */ })
flatMap(function (element, index, array) { /* … */ })
flatMap(function (element, index, array) { /* … */ }, thisArg)
});
```
&emsp; So, the above issue can be solved by `flatMap()` as

```JavaScript
const variantsArray = productsArray.flatMap(product => product.variants))
console.log(variantsArray)
```

Output will be

```JavaScript
[
  { color: 'red', size: 'S' },
  { color: 'blue', size: 'M' },
  { color: 'green', size: 'L' },
  { color: 'black', size: 'XL' },
  { color: 'pink', size: 'S' },
  { color: 'purple', size: 'M' }
]
```

&emsp; Instead of returning required properties from the array of objects in a `map()` method and then applying `flat()` to get a simple array of objects (in the above usecase), we made use of `flatMap()` and extracted only the variants array in each object to a single array of objects.

## Browser Compatibility

| Browser         | &nbsp;Version     |
|------------------|-------------|
| Google Chrome    | 69 and above |
| Edge             | 79 and above |
| Firefox          | 62 and above (Note: This function is available in Firefox Nightly only.) |
| Opera            | 56 and above |
| Safari           | 12 and above |

## Conclusion

&emsp; The `flatMap()` method is a powerful addition to JavaScript, allowing developers to simplify their code and perform complex operations on arrays and iterable objects with ease.

(Please do let me know on what topics to cover in the comments. Thanks)
