# April 17th 2018

## React Review -- Showing Content Conditionally

Since React is just JavaScript, variables can be set up to hide and show data the same way any conditional would displayed in a JavaScript application.

As an example, a *persons* variable can be initial set to null:
```js
let persons = null;
```

Then, based on a condition, JSX can be set to the variable:
```jsx
if (this.state.showPersons) {
    persons = (
        <div>
            {this.state.persons.map((person, index) => {
                return <Person
                    key={person.id}
                    click={() => this.deletePersonHandler(index)}
                    name={person.name}
                    changed={(event) => this.nameChangedHandler(event, person.id)}
                    age={person.age} />
            })}
        </div>
    );
}
```

For the example above, *showPersons* exist within the component's state and, depending on if it is **true** or **false**, the *persons* variable is either *null* or set to the JSX.

To display this, backet notation can be used within the *return* statement:
```jsx
return (
    <div className="App">
        <h1>I'm a React app</h1>
        <button
            style={style}
            onClick={this.togglePersonsHandler}>Toggle Names
        </button>
        {persons} <!-- persons rendered here -->
    </div>
);
```