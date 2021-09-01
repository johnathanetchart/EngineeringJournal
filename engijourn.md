//I will go through and adjust the formatting soon, using markdown etc to make it look nice. but for now, I think it's important to get started with writing my thoughts.
//"The best time to plant a tree was 20 years ago. The 2nd best time to plant a tree is right now" -- chinese proverb

9/1/2021
I am reviewing for a technical interview to identify gaps in my knowledge, mostly in terms of things that I had done before but had just forgotten. Those, I find, are the most frustrating to get hit with during an interview. While reviewing hash maps today, I accidentally happened upon the Map data structure that came into JavaScript with ES6. Essentially, it's just an object class, with some key differences. The main benefit I found pretty awesome is that it retains insertion, which I can imagine being incredibly helpful. It also has some other methods built into it such as size for getting the size, clearing for deleting everything from the Map, 'has' for checking existence of keys, a class based instantiation, and the ability to merge Maps. I'll definitely be using these in my current and future projects.

Examples Instantiations:
const first = new Map([
  [1, 'one'],
  [2, 'two'],
  [3, 'three'],
])
const second = new Map([
  [1, 'uno'],
  [2, 'dos']
])

Merging example:
// Merge maps with an array. The last repeated key wins.
const merged = new Map([...first, ...second, [1, 'eins']])

console.log(merged.get(1)) // eins
console.log(merged.get(2)) // dos
console.log(merged.get(3)) // three

Link to MDN:
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map

I also learned about the ability to swap array elements in place with ES6. Prior to this, I would always have to set up a temporary variable to hold one element, set the element at that index to the element at the 2nd index, then set the element at the 2nd index to the temporary variable's value. This new way is much cleaner and can take care of that in one line.

const arr = [1, 2, 3, 4, 5];

[(arr[0], arr[3])] = [arr[3], arr[0]]

console.log(arr) // [4, 2, 3, 1, 5]

