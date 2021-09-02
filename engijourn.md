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


Heap Data Structure notes:
I looked up binary heaps because I wanted to review them and solidify my knowledge of them. Basically a heap can be either a min heap or a max heap, moving either smaller or larger values up the tree structure respectively. When adding a value to the tree, it must fill the current row of the binary tree one at a time before moving to the next level, adding the inserted node as a child of the node that corresponds to the inserted index. This whole structure is displayed as an array, for simplicity. A cool little tip that helped me get the math down easier was:
1. starting the tree at index 1 instead of 0, leaving 0's value as null, simplifies a LOT of the math.
2. at any index i, left child's index = i * 2
3. at any index i, right child's index = i * 2 + 1
4. at any index i, parent's index = Math.floor(i /2) //to rounding is to account for odd indexes.


Thursday, September 2, 2021
While reviewing basic JavaScript syntax, specifically ES6, I was reminded that arrow function do not bind 'this'.

let hero = {
    _name: 'Billy Bob',
    failedGetSecretIdentity: () => {
        console.log(this) // this is the Window
        return this._name;
    },
    realGetSecretIdentity: function() {
      console.log(this) // this is the hero object
      return this._name;
    }
}
hero.failedGetSecretIdentity()

in the above object, the 'this' at the time the arrow function gets called is bound to the window, or the global object, but the function declaration version binds correctly to the object and will return the correct value. I'll have to be more mindful of this behavior in the future.

Arrow functions do not have:
  this
  arguments
so
  call
  apply
  bind
are NOT suitable for them.

If 'this' is important, use traditional function declaration.

/////
I had heard that id allocation is a common question for Dropbox interviews so I looked into it. I thought about it and figured that function would need some kind of storage to keep track of where it was in ID allocation and I figured for simplicity it could be an auto incrementing ID. My first thoughts led towards memoization. That type of function stores all of its values for quick access, but the main part that interested me was the storage within the function. I definitely needed a bit of a refresher on it but after a less-than-last-time amount of time I was able to both understand memoization again and also repurpose its functionality to create and id allocation function.

let allocateId = function() {
    let nextId = 0;
    //everything up here is within the scope of the returned function
    return () => {
        let result = nextId;
        nextId++;
        return result;
    }
}
let newAllocation = allocateId(); //instantiates a new instance for allocation.
console.log('1st user id:', newAllocation()); // logs 0
console.log('2nd user id:', newAllocation()); // logs 1
console.log('3rd user id:', newAllocation()); // logs 2
console.log('4th user id:', newAllocation()); // logs 3
console.log('5th user id:', newAllocation()); // logs 4


I also think that a class can work just as well and even allow inputting methods to store all ids, create them via a hash, get all allocated ids, etc. Here is what I came up with in a few minutes:

//class version
class IdClass {
    constructor() {
        this.nextId = 0;
        this.storedIds = [];
    }
    allocateId() {
        let id = this.nextId;
        this.nextId++;
        this.storedIds.push(id);
        return id;
    }
    listIds() {
        return this.storedIds;
    }

}

let classIdAllocation = new IdClass;
console.log(classIdAllocation.allocateId());
console.log(classIdAllocation.allocateId());
console.log(classIdAllocation.allocateId());
console.log(classIdAllocation.allocateId());
console.log(classIdAllocation.allocateId());

console.log(classIdAllocation.listIds());