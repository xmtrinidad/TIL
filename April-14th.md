# April 14th, 2018

## Working With Immutable Strings

In JavaScript strings are immutable.  Common functions like slice() and replace() create new strings.  Today I was reminded of this when attemping a challenge from Codefights that required changing a letter in a string to its next letter in the English alphabet.

My original attempt was to do something like below within a for loop:
```js
inputString[i] = nextLetter;
```

But this would not work because, as mentioned, strings are immutable.  To achieve the desired result I had to create a new string:
```js
// String builders
const lettersBefore = inputString.substring(0, i);
const nextLetter = String.fromCharCode(charCode+1);
const restOfLetters = inputString.substring(i + 1);

// New string with next letter
inputString = lettersBefore + nextLetter + restOfLetters;
```

---

## React Review - Working with Click Events

I've started to review React again as I prepare to work on my next project using it.  I had trouble getting click events to console.log the clicked item that exist within a child component but, after doing some research (Stack Overflow), I figured it out:

**Parent Component**        
The App component is the parent component in this example:

```js
<div className="App">
    <div className="container">
        <ItemMenu
            click={this.selectItem}
            items={this.state.items} />
    </div>
</div>
```

As shown above, the ```<ItemMenu>``` has a click attribute that refernces the selectItem() function within the parent component:

```js
selectItem = (data) => {
    console.log(data);
};
```

The clicked item will be passed into this function from whatever item is clicked inside the ```<ItemMenu>```:

**ItemMenu Component**      
```js
const itemMenu = (props) => {
    const handleClick = (item) => {
      props.click(item);
    };

    const list = props.items.map((item, i) =>
        <li key={item.name}
            onClick={() => handleClick(item)}
            className={"ItemMenu__item " + (item.selected ? 'selected' : '')}>
            <i className={item.icon + " ItemMenu__item-icon"}/>
            <span className="mt-2 ItemMenu__item-text">{item.name}</span>
        </li>);
    return (
        <ul className="ItemMenu">
            {list}
        </ul>
    )
};
```

For each ```<li>``` created from the map function, an *onClick* attribute is added that references the *handleClick()* function within the component.  The prevent the function from running, an anonymous function is used:
 ```() => handleClick(item)```

 When the item is clicked, the *handleClick()* function runs, which then uses the *props* passed into the component then access the click attribute given to it from the parent component.  
 
 As shown earlier, the *click* attribute from the parent component takes in a *data* argument that is then passed to the parent component *selectItem()* function.

 ---