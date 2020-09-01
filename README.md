# About
Having fun here getting a little sharper with Javascript :)  
For Codewars, problems are measured by a kyu level, the smaller the number, the more difficult  

## Recursion 101  
Aug 31  
https://www.codewars.com/kata/514a024011ea4fb54200004b  

I wanted to try solving this without using Regex, because it might have been less fun using it.
This works for the base cases, but the extended tests break it. Will refactor tomorrow.
```js
function domainName(url){
  
  let indexOfDomainStart = 0;
  let indexOfDomainEnd = 0;
  
  for (let i = 0; i < url.length; i++) {
    if (!indexOfDomainStart && url.slice(i, i + 2) === "//" && url.slice(i + 2, i + 6) === "www.") {
      // found http://www.
      indexOfDomainStart = i + 6;
    } else if (!indexOfDomainStart && url.slice(i, i + 4) === "www.") {
      // found only www.
      indexOfDomainStart = i + 4;
    } else if (!indexOfDomainStart && url.slice(i, i + 2) === "//") {
      // found only http:// or https://
      indexOfDomainStart = i + 2;
    } else if (indexOfDomainStart && url[i] === "." && i !== 3) {
      // found the punctuation after the domain. Note: subdomains would break this.
      indexOfDomainEnd = i
      break;
    } else {
    }
  }
  return url.slice(indexOfDomainStart, indexOfDomainEnd)
}
```

## Recursion 101  
Aug 29  
https://www.codewars.com/kata/5b752a42b11814b09c00005d/solutions/javascript  

```js
function solve(a,b){
    if (a == 0 || b == 0) {
      return [a,b]
    } else if (a >= 2*b) {
      a = a - 2*b;
      return solve(a,b);
    } else if (b >= 2*a) {
      b = b - 2*a;
      return solve(a,b);
    } else {
      return ([a,b])
    }
}
```

## Recursive Replication  
Aug 27  
https://www.codewars.com/kata/57547f9182655569ab0008c4  

Refactored (with concat)  
```js
function replicate(times, number) {
  if (times > 0) {
    return [number].concat(replicate(times - 1, number))
  } else {
    return []
  }
}
```

Original  
```js
function replicate(times, number) {
  let array = []
  
  function populateArrayByTimeAmount(times, number) {
      if (times < 0) {
      } else if (times === 0) {
      } else if (times === 1) {
        array.push(number)
      } else {
        array.push(number)
        populateArrayByTimeAmount(times - 1, number)
      }
  }
  
  populateArrayByTimeAmount(times, number)
  
  return array
}
```

## Apple Stocks  
Aug 10  
https://www.interviewcake.com/question/javascript/stock-price?course=fc1&section=greedy  

```
```

## Unary function chainer  
6 kyu  
Aug 7  
https://www.codewars.com/kata/54ca3e777120b56cb6000710   

```
```

## Rot13
5 kyu  
Aug 5  
https://www.codewars.com/kata/530e15517bc88ac656000716  

Certainly don't enjoy mapping out the letters, but it might be necessary?... Will refactor
```js
function rot13(message){
  let lettersByPosition = [
    [1, 'a'],
    [2, 'b'],
    [3, 'c'],
    [4, 'd'],
    [5, 'e'],
    [6, 'f'],
    [7, 'g'],
    [8, 'h'],
    [9, 'i'],
    [10, 'j'],
    [11, 'k'],
    [12, 'l'],
    [13, 'm'],
    [14, 'n'],
    [15, 'o'],
    [16, 'p'],
    [17, 'q'],
    [18, 'r'],
    [19, 's'],
    [20, 't'],
    [21, 'u'],
    [22, 'v'],
    [23, 'w'],
    [24, 'x'],
    [25, 'y'],
    [26, 'z']
  ];
  let positionByLetters = [
    ['a', 1],
    ['b', 2],
    ['c', 3],
    ['d', 4],
    ['e', 5],
    ['f', 6],
    ['g', 7],
    ['h', 8],
    ['i', 9],
    ['j', 10],
    ['k', 11],
    ['l', 12],
    ['m', 13],
    ['n', 14],
    ['o', 15],
    ['p', 16],
    ['q', 17],
    ['r', 18],
    ['s', 19],
    ['t', 20],
    ['u', 21],
    ['v', 22],
    ['w', 23],
    ['x', 24],
    ['y', 25],
    ['z', 26]
  ];
  let byPositionMap = new Map(lettersByPosition);
  let byLetterMap = new Map(positionByLetters);
  
  encodedCaesarStyle = message.split('').map(letter => {
    let newPosition = 0;
    // set default letter, in case it's puncutation or a space, etc
    let newLetter = letter;
    // check if letter is uppercase
    let upperCase = false;
    if (letter === letter.toUpperCase()) {upperCase = true;}
    
    // first, check if letter is a valid English alphabet letter
    if (byLetterMap.has(letter.toLowerCase())) {
      
      upperCase ? alphabetPosition = byLetterMap.get(letter.toLowerCase()) : alphabetPosition = byLetterMap.get(letter);
      
      // if adding 13 takes the letter past 26 (the last valid letter), let's figure out a remainder first
      if (alphabetPosition > 13) {
        let total = alphabetPosition + 13;
        // use modulo to determine the remainder to count again from 0 or 'a'
        newPosition = total % 26;
      } else {
        newPosition = 13 + alphabetPosition
      }

      upperCase ? newLetter = byPositionMap.get(newPosition).toUpperCase() : newLetter = byPositionMap.get(newPosition)
    }
    return newLetter
  }).join('')
    
  return encodedCaesarStyle
}
```

## Word Cloud Data (Practice Interview Question) | Interview Cake
(Interview Cake)  
Aug 1
https://www.interviewcake.com/question/javascript/word-cloud?course=fc1&section=hashing-and-hash-tables  

Updated, tinkered a bit but started too late tonight - back at it tomorrow!
(hypens causing problems, but I want to avoid regex despite liking it)
```js
class WordCloudData {
  constructor(inputString) {
    this.wordsToCounts = new Map();
    this.populateWordsToCounts(inputString);
  }
  
  populateWordsToCounts(inputString) {
    console.log(inputString)
    let wordCounter = 0;
    let arrayOfWords = inputString.split(/-| /);
    arrayOfWords.forEach(word => {
        console.log(word[word.length - 1])
      if (word[word.length - 1] === '?' || word[word.length - 1] === '!'|| word[word.length - 1] === '.'){
        console.log('punctuation present!')
        word = word.slice(0, word.length - 1)
      }

      if (this.wordsToCounts.get(word) === undefined) {
        this.wordsToCounts.set(word, 1)
      } else {
        this.wordsToCounts.set(word, (this.wordsToCounts.get(word) + 1))
      }
      
    })
    console.log(this.wordsToCounts)
    return this.wordsToCounts
  }
```

## Permutation Palindrome (Practice Interview Question) | Interview Cake
(Interview Cake)  
July 30  
https://www.interviewcake.com/question/javascript/inflight-entertainment?course=fc1&section=hashing-and-hash-tables  
  
First green before checking recommended soltuion
```js
function hasPalindromePermutation(theString) {

  function checkIfPalindrome(string) {
    let leftIndex = 0;
    let rightIndex = string.length - 1;
    let isPalindrome = true
    
    while (leftIndex < rightIndex) {
      if (string[leftIndex] === string[rightIndex]) {
      } else {
        isPalindrome = false
        return isPalindrome;
      }
      leftIndex++
      rightIndex--
    }
    
    return isPalindrome;
  }

  const permutator = (inputArr) => {
    let permutations = [];
  
    const permute = (arr, m = []) => {
      if (arr.length === 0) {
        permutations.push(m)
      } else {
        for (let i = 0; i < arr.length; i++) {
          let curr = arr.slice();
          let next = curr.splice(i, 1);
          permute(curr.slice(), m.concat(next))
        }
      }
    }
  
    permute(inputArr)
    let result = permutations.map(combination => combination.join(''))
    
    return result;
  }
  
  
  const doesAPalindromeExist = permutator(theString.split('')).some(permutation => {
    if (checkIfPalindrome(permutation) === true) return true;
    else return false;
  })

  return doesAPalindromeExist;
}
```

Alternative approach to checkIfPalindrome 
```js
  function checkIfPalindrome(string) {
    let isPalindrome = false;
    
    let isEven = false;
    let isOdd = false;
    if (string.length % 2 === 0) {
      isEven = true;
    } {
      isOdd = true
    }
    
    isOdd ? leftSlice = string.slice(0, Math.trunc(string.length / 2)) : leftSlice = string.slice(0, Math.round(string.length / 2))
    isOdd ? rightSlice = string.slice(0, string.length / 2) : rightSlice = string.slice(0, string.length / 2)
    
    if (leftSlice === rightSlice.reverse())
      isPalindrome = true;
    
    return isPalindrome;
  }

  const permutator = (inputArr) => {
    let permutations = [];
  
    const permute = (arr, m = []) => {
      if (arr.length === 0) {
        permutations.push(m)
      } else {
        for (let i = 0; i < arr.length; i++) {
          let curr = arr.slice();
          let next = curr.splice(i, 1);
          permute(curr.slice(), m.concat(next))
        }
      }
    }
  
    permute(inputArr)
    let result = permutations.map(combination => combination.join(''))
    
    return result;
  }
  
  
  const doesAPalindromeExist = permutator(theString.split('')).some(permutation => {
    if (checkIfPalindrome(permutation) === true) return true;
    else return false;
  })

  return doesAPalindromeExist;
}
```

## Inflight Entertainment (Practice Interview Question) | Interview Cake
(Interview Cake)  
July 27  
https://www.interviewcake.com/question/javascript/inflight-entertainment?course=fc1&section=hashing-and-hash-tables  
```js
function canTwoMoviesFillFlight(movieLengths, flightLength) {

  // Determine if two movie runtimes add up to the flight length
  console.log(movieLengths.sort())
  console.log(flightLength)
  
  let movieSum = 0;
  
  if (movieLengths.length === 0) {
    return false;
  } else if (movieLengths.length === 1) {
    return false;
  } else {
    sortedMovies = movieLengths.sort();
    movieSum = sortedMovies[0] + sortedMovies[1];
  }
  
  if (movieSum <= flightLength) return true;
  console.log('not true')
  return false;
}
```

The recommended solution. First time using a Set in JS
```js
function canTwoMoviesFillFlight(movieLengths, flightLength) {

  // Determine if two movie runtimes add up to the flight length
  
  const movieLengthsSeen = new Set();
  
  for (let i = 0; i < movieLengths.length; i++) {
    const firstMovieLength = movieLengths[i];
    
    const matchingSecondMovieLength = flightLength - firstMovieLength;
    if (movieLengthsSeen.has(matchingSecondMovieLength)) {
      return true;
    }
    movieLengthsSeen.add(firstMovieLength);
  }
  
  return false;
}
```

## Cafe Order Checker (Practice Interview Question) | Interview Cake  
(Interview Cake)  
July 26  
https://www.interviewcake.com/question/javascript/cafe-order-checker?course=fc1&section=array-and-string-manipulation  
  
Refactored
```js
function isFirstComeFirstServed(takeOutOrders, dineInOrders, servedOrders) {

  let takeOutNotEmpty = takeOutOrders.length >= 1;
  let dineInNotEmpty = dineInOrders.length >= 1;
  let totalDineInTakeOut = takeOutOrders.length + dineInOrders.length;
  let takeOutIndex = 0;
  let dineInIndex = 0;
  let servedOrdersIndex = 0;
  
  if (totalDineInTakeOut !== servedOrders.length) {return false;}
  
  while (servedOrdersIndex < totalDineInTakeOut) {
    let currentOrder = servedOrders[servedOrdersIndex]
    
    if (takeOutNotEmpty && currentOrder === takeOutOrders[takeOutIndex]) {
      takeOutIndex++;
    } else if (dineInNotEmpty && currentOrder === dineInOrders[dineInIndex]) {
      dineInIndex++;
    } else {
      return false;
    }
    
    servedOrdersIndex++
  }
  
  return true;
}
```
  
Green before refactor
```js
function isFirstComeFirstServed(takeOutOrders, dineInOrders, servedOrders) {

  // Check if we're serving orders first-come, first-served
  
  const takeOutNotEmpty = takeOutOrders.length >= 1;
  const dineInNotEmpty = dineInOrders.length >= 1;
  
  let takeOutIndex = 0;
  let dineInIndex = 0;
  let totalDineInTakeOut = takeOutOrders.length + dineInOrders.length;
  let servedOrdersIndex = 0;
  let loopCounter = 0;
  
  if (totalDineInTakeOut !== servedOrders.length) {return false;}
  
  while ( servedOrdersIndex < (totalDineInTakeOut) ) {

    if ((dineInNotEmpty || takeOutNotEmpty) && servedOrders[servedOrdersIndex] === takeOutOrders[takeOutIndex]) {
      takeOutIndex++;
      servedOrdersIndex++;
    } else if ((dineInNotEmpty || takeOutNotEmpty) && servedOrders[servedOrdersIndex] === dineInOrders[dineInIndex]) {
      dineInIndex++;
      servedOrdersIndex++;
    } else {
      return false;
    }
  }
  
  return true;
}
```

## Merge Sorted Arrays
(Interview Cake)  
July 24  
https://www.interviewcake.com/question/javascript/merge-sorted-arrays?course=fc1&section=array-and-string-manipulation  

First 'green' before refactoring
```js
function mergeArrays(myArray, alicesArray) {

  // Combine the sorted arrays into one large sorted array
  let mergedArray = []
  
  //help function to check if an element exists, helps with arrays of different lengths
  function checkIfExists (arrayToCheck, arrayToCheckIndex, backupArray, backupArrayIndex) {
    arrayToCheck[arrayToCheckIndex] ? mergedArray.push(arrayToCheck[arrayToCheckIndex]) : mergedArray.push(backupArray[backupArrayIndex])
  }
  
  //help function to check if an element exists, helps with arrays of different lengths
  function checkForEmptyArrays (arrayOne, arrayTwo) {
    if (arrayOne.length === 0 && arrayTwo.length === 0) {return null}
    if (arrayOne.length === 0) {mergedArray = arrayTwo}
    if (arrayTwo.length === 0) {mergedArray = arrayOne}
  }
  
  function combArraysAndMerge (arrayOne, arrayTwo) {
    arrayOneIndex = 0;
    arrayTwoIndex = 0;
    totalOrders = arrayOne.length + arrayTwo.length;
    
    i = 0;
    while (i < totalOrders) {
      //from the current arrays, compare which number is greater, add it, then increase the index for that array
      if (arrayOne[arrayOneIndex] < arrayTwo[arrayTwoIndex]){
        checkIfExists(arrayOne, arrayOneIndex, arrayTwo, arrayTwoIndex)
        arrayOneIndex++
      } else {
        checkIfExists(arrayTwo, arrayTwoIndex, arrayOne, arrayOneIndex)
        arrayTwoIndex++
      }
      i++
    }
    checkForEmptyArrays(arrayOne, arrayTwo)
  }
  
  combArraysAndMerge(myArray, alicesArray)

  return mergedArray;
}
```

The recommended solution.  
Here the 'isArrayExhausted' variable helps to account for what I was accomplising with the less clean 'checkForEmptyArrays'  
```js
function mergeArrays(myArray, alicesArray) {
  const mergedArray = [];

  let currentIndexAlices = 0;
  let currentIndexMine = 0;
  let currentIndexMerged = 0;

  while (currentIndexMerged < (myArray.length + alicesArray.length)) {

    const isMyArrayExhausted = currentIndexMine >= myArray.length;
    const isAlicesArrayExhausted = currentIndexAlices >= alicesArray.length;

    if (!isMyArrayExhausted && (isAlicesArrayExhausted ||
      (myArray[currentIndexMine] < alicesArray[currentIndexAlices]))) {

      mergedArray[currentIndexMerged] = myArray[currentIndexMine];
      currentIndexMine++;
    } else {
      mergedArray[currentIndexMerged] = alicesArray[currentIndexAlices];
      currentIndexAlices++;
    }

    currentIndexMerged++;
  }

  return mergedArray;
}

```

## Regex Password Validation
5 kyu  
July 8
https://www.codewars.com/kata/52e1476c8147a7547a000811  

```
```

---

## Human Readable Time  
5 kyu  
June 30  
https://www.codewars.com/kata/52685f7382004e774f0001f7  

```
```

## String incrementer  
June 29  
https://www.codewars.com/kata/54a91a4883a7de5d7800009c  

```
```

## Reverse Words
(Interview Cake)  
June 28  
https://www.interviewcake.com/question/javascript/reverse-words?course=fc1&section=array-and-string-manipulation  
  
This is absolutely some of the hackiest code I've ever written. It worked but..., not ideal :)
```js
function reverseWords(message) {
  // Decode the message by reversing the words
  // console.log(message)
  if (message[0]) {
        let wordStorage = {}
    let wordCounter = 1
    
    //stuff the object with all the words
    message.map(element => {
      if (element !== ' ') {
        wordStorage[wordCounter] ? wordStorage[wordCounter] += element : wordStorage[wordCounter] = element
      } else {
        wordCounter++
      }
    })
    
    //access the words by keys, 1, 2, 3 corresponding to the order the words were found
    let arrayI = 0;
    for (let objectI = wordCounter; objectI > 0; objectI--){
      if (objectI !== 1) {
        for (let i = 0; i < wordStorage[objectI].length; i++) {
          message[arrayI] = wordStorage[objectI][i]
          arrayI++
        }
        message[arrayI] = ' '
        arrayI++
      } else {
        for (let i = 0; i < wordStorage[objectI].length; i++) {
          message[arrayI] = wordStorage[objectI][i]
          arrayI++
        }
      }
    }
```

Refactor here after studying other solutions
```js
function reverseWords(message) {
  //challenge here is to reverse all the words 'IN PLACE'

  //helper function to reverse all the characters
    function reverseCharacters(message, leftIndex, rightIndex){
    while (leftIndex < rightIndex) {
      
      const temp = message[leftIndex];
      message[leftIndex] = message[rightIndex];
      message[rightIndex] = temp;
      leftIndex++;
      rightIndex--;
    }
  }

  //reverse them initially
  reverseCharacters(message, 0, message.length - 1)
  
  //now, reverse per word (identify by spaces)
  let currentWordIndex = 0;
  for (let i = 0; i <= message.length; i++) {
    if (i === message.length || message[i] === ' ') {
      reverseCharacters(message, currentWordIndex, i - 1)
      currentWordIndex = i + 1
    }
  }
}
```

## Reverse String in Place
(Interview Cake)  
June 23  
https://www.interviewcake.com/question/javascript/reverse-string-in-place?course=fc1&section=array-and-string-manipulation

```js
function reverse(array) {

  let leftIndex = 0;
  let leftIndex = array.length - 1;
  
  while (leftIndex < rightIndex) {
    let tempToSwap = array[leftIndex];
    array[leftIndex] = array[rightIndex];
    array[rightIndex] = tempToSwap
    
    leftIndex++;
    rightIndex--;
  }

}
```

## Merge Meeting Times
(Interview Cake)  
June 20  
https://www.interviewcake.com/question/javascript/merging-ranges?course=fc1&section=array-and-string-manipulation

In my initial approach, I tried adding this helper function... Nope :) Was not optimal.
```js
function mergeRanges(meetings) {

  //helper function
  function checkForTimeOverlap (a_startTime, a_endTime, b_startTime, b_endTime) {
    if (a_endTime >= b_startTime && a_endTime <= b_endTime) return 'a_then_b';
    if (b_endTime >= a_startTime && b_endTime <= a_endTime) return 'b_then_a';
    if (b_startTime <= a_startTime && a_startTime <= b_startTime) return 'a_within_b';
    if (a_startTime <= b_startTime && b_endTime <= a_endTime) return 'b_within_a';
  }
  
  //will do either a filter to create a new array of only merged objects and single meetings, or mutate original object
  const optimizedMeetingSchedule = [];
  
  meetings.forEach(meeting => {
    console.log(meeting)
  })
  
  return optimizedMeetingSchedule;
}

```

A solution
```js
function mergeRanges(meetings) {

  //copy, then sort array by start times
  const meetingsCopy = JSON.parse(JSON.stringify(meetings));
  const sortedMeetings = meetingsCopy.sort((a, b) => a.startTime - b.startTime);

  const optimizedMeetings = [sortedMeetings[0]];
  
  meetingsCopy.forEach((meeting, i) => {
    console.log(meeting)
    const currentMeeting = sortedMeetings[i];
    const lastMergedMeeting = optimizedMeetings[optimizedMeetings.length - 1];
    
    if (currentMeeting.startTime <= lastMergedMeeting.endTime) {
      lastMergedMeeting.endTime = Math.max(lastMergedMeeting.endTime, currentMeeting.endTime);
    } else {
      optimizedMeetings.push(currentMeeting);
    }
  })
  
  return optimizedMeetings;
}
```

---

## Multi-tap Keypad Text Entry on an Old Mobile Phone
June 18  
https://www.codewars.com/kata/54a2e93b22d236498400134b

```
```

---

## Top Scores (Practice Interview Question)
June 17  
https://www.interviewcake.com/question/javascript/top-scores

I was able to do this with .sort...  
I'm assuming this question was created before the JS version that .sort was introduced in...
```js
function sortScores(unorderedScores, highestPossibleScore) {
  unorderedScores.sort((a, b) => b - a);
  return unorderedScores;
}

```  

The non-sort solution  
I had to throw in a lot of console.logs to make sense of it at first
```js
function sortScores(unorderedScores, highestPossibleScore) {
  // Sort the scores in O(n) time
  const scoreCounts = new Array(highestPossibleScore + 1).fill(0);
  unorderedScores.forEach(score => {
    scoreCounts[score]++;
  })
  
  const sortedScores = [];
  for (let score = highestPossibleScore; score >= 0; score--) {
    const count = scoreCounts[score];
    for (let time = 0; time < count; time++){
      sortedScores.push(score);
    }
  }
  
  return sortedScores;
}
```

---

## The Supermarket Queue
6 kyu  
June 16  
https://www.codewars.com/kata/57b06f90e298a7b53d000a86  

First submit, before refactoring
```js
function queueTime(customers, n) {
  const currentWaitsInLines = new Array(n).fill(0);
  
  const getMinimumInArray = array => {
    return Math.min.apply( Math, array );
  }
  
  const getMaximumInArray = array => {
    return Math.max.apply( Math, array );
  }

  if (customers[0]) {
    for (let totalCustomerNumber = customers.length; customers[0];){
    const firstInLine = customers.shift();
    currentWaitsInLines[currentWaitsInLines.findIndex(element => element == getMinimumInArray(currentWaitsInLines))] += firstInLine;
    }
    
    return getMaximumInArray(currentWaitsInLines)
  } else {
    return 0
  }
  
}
```

```
```

---

## Reverse or rotate?
6 kyu  
June 16  
https://www.codewars.com/kata/56b5afb4ed1f6d5fb0000991

```
```

---

## longest_palindrome
6 kyu  
June 15  
https://www.codewars.com/kata/54bb6f887e5a80180900046b

```
```

---

## 1282. Group the People Given the Group Size They Belong To
Medium  
June 14  
https://leetcode.com/problems/group-the-people-given-the-group-size-they-belong-to/

```
```

---

## Adjacent repeated words in a string
6 kyu  
June 13  
https://www.codewars.com/kata/5245a9138ca049e9a10007b8

```js
function countAdjacentPairs(searchString) {
  let regexSearchForDuplicate = /\b(\w+)\b\s+\1\b\s*(\1\b\s)*/gi;
  try {
    return duplicateCounter = searchString.match(regexSearchForDuplicate||[]).length
  } catch (error) {
      return 0
  }
}
```

---

## Word a10n (abbreviation)
6 kyu  
June 12  
https://www.codewars.com/kata/5375f921003bf62192000746

in progress
```js
function abbreviate(string) {
  let newString = ""
  if (string.length > 4) {
    let middleCharacters = string.length - 2
    console.log(middleCharacters)
    newString = string.replace(/\B[a-z]*\B/, `${middleCharacters}`)
  }
  
  return newString
}
```

---

## Persistent Bugger
6 kyu  
June 11  
https://www.codewars.com/kata/55bf01e5a717a0d57e0000ec

```js
function persistence(num) {
  let stringedNumber = num.toString();
  let multipliedNumber = 0;
  let multiplyCounter = 0;
  
  while (stringedNumber.length != 1) {
    let separatedNumbers = []
    for (var i = 0; i < stringedNumber.length; i += 1) {
      separatedNumbers.push(parseInt(stringedNumber.charAt(i)))
    }
    multipliedNumber = separatedNumbers.reduce((acc, val) => acc *= val);
    stringedNumber = multipliedNumber.toString();
    multiplyCounter++;
  }
  
  return multiplyCounter
}
```

---

## Disemvowel Trolls
7 kyu  
June 11  
https://www.codewars.com/kata/52fba66badcd10859f00097e

```js
function disemvowel(str) {
  return str.replace(/[aeiou]/gi, '');
}
```

---

## Two Sum
6 kyu  
June 10  
https://www.codewars.com/kata/52c31f8e6605bcc646000082

```js
function twoSum(numbers, target) {
  let firstI = 0;
  let secondI = 0;
  let fired = false;
  numbers.forEach((firstNumber, firstIndex) => {
    numbers.forEach((secondNumber, secondIndex) => {
      if (firstIndex != secondIndex && firstNumber + secondNumber == target && fired != true){
        firstI = firstIndex;
        secondI = secondIndex;
        fired = true;
      }
    })
  })
  return [firstI, secondI];
}
```
---

## Break camelCase
6 kyu  
June 9  
https://www.codewars.com/kata/5208f99aee097e6552000148

```js
function solution(string) {
    let separated = "";
    for (var i = 0; i < string.length; i++) {
      if (string[i] == string[i].toUpperCase()){
        separated += ` ${string[i]}`;
      } else {
        separated += string[i];  
      }
    }
    return separated;
}
```

---

## Count the smiley faces!
6 kyu  
June 4  
https://www.codewars.com/kata/583203e6eb35d7980400002a

---

## Snakes and Ladders
Starting May 29, back in the city after a mountain hiatus  
https://www.codewars.com/kata/587136ba2eefcb92a9000027

---

## Beeramid
Starting May 27, from a vacation cabin in the mountains  
https://www.codewars.com/kata/51e04f6b544cf3f6550000c1

> Let's pretend your company just hired your friend from college and paid you a referral bonus. Awesome! To celebrate, you're taking your team out to the terrible dive bar next door and using the referral bonus to buy, and build, the largest three-dimensional beer can pyramid you can. And then probably drink those beers, because let's pretend it's Friday too.
> 
> A beer can pyramid will square the number of cans in each level - 1 can in the top level, 4 in the second, 9 in the next, 16, 25...
> 
> Complete the beeramid function to return the number of complete levels of a beer can pyramid you can make, given the parameters of:
> 
> 1) your referral bonus, and
> 
> 2) the price of a beer can
> 
> For example:
> 
> beeramid(1500, 2); // should === 12
> beeramid(5000, 3); // should === 16

---

## A simple Tic-tac-toe class
My friend who's a decent coder said this had him freeze up during a tech interview.  
Starting May 22  
https://www.codewars.com/kata/529b9ec8064ec38636000134

---

## The Hashtag Generator
Completed May 21 2020  
https://www.codewars.com/kata/52449b062fb80683ec000024/train/javascript

#### Solution 1 (before a final refactor)
```js
function generateHashtag (str) {
  let emptyOrLongerThan140Char = false;
  let newString = "";
  str[0] && (str.split(' ').join('').length > 0) ? null : emptyOrLongerThan140Char = true;
  
  if (!emptyOrLongerThan140Char) {
    newString = '#' + str.replace(/  +/g, ' ').split(' ').map(word => word[0].toUpperCase() + word.slice(1, word.length)).join('')
    newString.length > 140 ? emptyOrLongerThan140Char = true : null;
  } else {
    emptyOrLongerThan140Char = true;
  }

  return emptyOrLongerThan140Char ? false : newString
}
```

#### Solution 2 (refactored)
```js
function generateHashtag (str) {
  if(!str || str[0] === "") return false;

  let newString = '#' + str.replace(/  +/g, ' ').split(' ').map(word => {
    if (word) {
      return word[0].toUpperCase() + word.slice(1, word.length)
    }
    }).join('')

  return (newString.length > 140 || newString.length == 1) ? false : newString
}
```

---

## Are they the "same"?
Completed May 2020  
https://www.codewars.com/kata/550498447451fbbd7600041c

> Given two arrays a and b write a function comp(a, b) (compSame(a, b) in Clojure) that checks whether the two arrays have the "same" elements, with the same multiplicities. "Same" means, here, that the elements in b are the elements in a squared, regardless of the order.
> Examples
> Valid arrays
> 
> a = [121, 144, 19, 161, 19, 144, 19, 11]  
> b = [121, 14641, 20736, 361, 25921, 361, 20736, 361]
> 
> comp(a, b) returns true because in b 121 is the square of 11, 14641 is the square of 121, 20736 the square of 144, 361 the square of 19, 25921 the square of 161, and so on. It gets obvious if we write b's elements in terms of squares:
> 
> a = [121, 144, 19, 161, 19, 144, 19, 11] 
> b = [11*11, 121*121, 144*144, 19*19, 161*161, 19*19, 144*144, 19*19]
> 
> Invalid arrays
> 
> If we change the first number to something else, comp may not return true anymore:
> 
> a = [121, 144, 19, 161, 19, 144, 19, 11]  
> b = [132, 14641, 20736, 361, 25921, 361, 20736, 361]
> 
> comp(a,b) returns false because in b 132 is not the square of any number of a.
> 
> a = [121, 144, 19, 161, 19, 144, 19, 11]  
> b = [121, 14641, 20736, 36100, 25921, 361, 20736, 361]
> 
> comp(a,b) returns false because in b 36100 is not the square of any number of a.
> Remarks
> 
>     a or b might be [] (all languages except R, Shell).
>     a or b might be nil or null or None or nothing (except in Haskell, Elixir, C++, Rust, R, Shell, PureScript).
> 
> If a or b are nil (or null or None), the problem doesn't make sense so return false.
> Note for C
> 
> The two arrays have the same size (> 0) given as parameter in function comp.
> 

#### Solution 1 (checking for null inputs in the return)
```js
function comp(array1, array2){
  const checkForFalses = () => {
    var onlyTrues = true;
    array1.forEach(number => {
      if (!array2.includes(number ** 2)) {
        onlyTrues = false;
      } else {
        array2.splice([array2.findIndex(num => num === (number ** 2))], 1);
      }
    })
    return onlyTrues;
  }
  return array1 && array2 ? checkForFalses() : false;
}
```


#### Solution 2 (checking for null inputs prior to returning)
```js
function comp(array1, array2){
  var onlyTrues = true;
  if (!array1 || !array2) {
    return false;
  }
  array1.forEach(number => {
    if (!array2.includes(number ** 2)) {
      onlyTrues = false;
    } else {
      var currentNumberSquaredIndex = array2.findIndex(num => num === (number ** 2));
      array2.splice([currentNumberSquaredIndex], 1);
    }
  })
  return onlyTrues;
}
```

---

## Format a string of names like 'Bart, Lisa & Maggie'.
Completed May 2020  
https://www.codewars.com/kata/53368a47e38700bd8300030d

> Given: an array containing hashes of names
> 
> Return: a string formatted as a list of names separated by commas except for the last two names, which should be separated by an ampersand.
> 
> Example:
> 
> list([ {name: 'Bart'}, {name: 'Lisa'}, {name: 'Maggie'} ])
> // returns 'Bart, Lisa & Maggie'
> 
> list([ {name: 'Bart'}, {name: 'Lisa'} ])
> // returns 'Bart & Lisa'
> 
> list([ {name: 'Bart'} ])
> // returns 'Bart'
> 
> list([])
> // returns ''
> 
> Note: all the hashes are pre-validated and will only contain A-Z, a-z, '-' and '.'.

#### Solution
```js
function list(names){
  var namesToJoin = [];
  names.forEach(name => namesToJoin.push(name["name"]));
  var formattedNames = namesToJoin.join(", ").replace(/,([^,]*)$/, ' &' + '$1');
  return formattedNames;
}
```

---

## My Languages
Completed April 2020  
https://www.codewars.com/kata/5b16490986b6d336c900007d

> Your task
> 
> You are given a dictionary/hash/object containing some languages and your test results in the given languages. Return the list of languages where your test score is at least 60, in descending order of the results.
> 
> Note: the scores will always be unique (so no duplicate values)
> Examples
> 
> {"Java": 10, "Ruby": 80, "Python": 65}    -->  ["Ruby", "Python"]
> {"Hindi": 60, "Dutch" : 93, "Greek": 71}  -->  ["Dutch", "Greek", "Hindi"]
> {"C++": 50, "ASM": 10, "Haskell": 20}     -->  []

#### Solution
```js
function myLanguages(results) {
  var sixtyOrHigherTest = Object.entries(results).filter(language => language[1] >= 60)
  return sixtyOrHigherTest.sort((a,b) => b[1] - a[1]).map(language => language[0]);
}
```

---

## Happy Birthday, Darling!
Completed April 2020  
https://www.codewars.com/kata/5e96332d18ac870032eb735f

> As you may know, once some people pass their teens, they jokingly only celebrate their 20th or 21st birthday, forever. With some maths skills, that's totally possible - you only need to select the correct number base!
> 
> For example, if they turn 32, that's exactly 20 - in base 16... Already 39? That's just 21, in base 19!
> 
> Your task is to translate the given age to the much desired 20 (or 21) years, and indicate the number base, in the format specified below.
> 
> Note: input will be always > 21
> Examples:
> 
> 32  -->  "32? That's just 20, in base 16!"
> 39  -->  "39? That's just 21, in base 19!"
> 
> Hint: if you may don't know (enough) about numeral systems and radix, just observe the pattern!

#### Solution
```js
function womensAge(n) {
  base = 1;
  
  while (n / base > 2) {
    base++;
    //make n / base doesn't go under 2
    if (n / base < 2){
    base--;
    break;
    }
  }
  
  if (n % base === 0 || n % base === 1){
  return `${n}? That's just 2${n % base}, in base ${base}!`
  }
}
```

---

## Sum of Digits / Digital Root
Completed March 2020  
https://www.codewars.com/kata/541c8630095125aba6000c00

> In this kata, you must create a digital root function.
> 
> A digital root is the recursive sum of all the digits in a number. Given n, take the sum of the digits of n. If that value has more than one digit, continue reducing in this way until a single-digit number is produced. This is only applicable to the natural numbers.
> 
> Here's how it works:
> 
> digital_root(16)
> => 1 + 6
> => 7
> 
> digital_root(942)
> => 9 + 4 + 2
> => 15 ...
> => 1 + 5
> => 6
> 
> digital_root(132189)
> => 1 + 3 + 2 + 1 + 8 + 9
> => 24 ...
> => 2 + 4
> => 6
> 
> digital_root(493193)
> => 4 + 9 + 3 + 1 + 9 + 3
> => 29 ...
> => 2 + 9
> => 11 ...
> => 1 + 1
> => 2

#### Solution
```js
function digital_root(n) {
  let currentNumbers = n
  let sum = 0
  console.log("num before loop", currentNumbers)

  while (currentNumbers >= 10) {
        sum = 0
        currentNumbers.toString().split('').forEach(num => {
          sum += parseInt(num)
        })
        currentNumbers = sum
  }
  console.log("num after loop", currentNumbers)
  return currentNumbers
}
```
