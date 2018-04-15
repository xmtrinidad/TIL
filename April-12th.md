# TIL - April 12th, 2018

## Angular -- Resetting Forms

While working on my MEAN Todo application, I wanted to reset a form.  This form doesn't use two-way binding, so I couldn't reset the strings when the form was submitted.  I did, however, reference the form when submitting it.

```js
onRegisterSubmit(f: NgForm) {
    // ... Other code

    f.reset({username: '', email: '', password: ''})
  }
```

The above code would reset the values to *null* and upon submitting again, an error would be thrown due to other code that validates the fields.  To reset the fields with empty strings, I had to pass in an object into the *reset()* method and set the values of the inputs to empty strings:

```js
onRegisterSubmit(f: NgForm) {
    // ... Other code

    f.reset({username: '', email: '', password: ''})
  }
```

---
