# April 4th, 2018

## Angular

### Reference an Angular form using Template drive approach

**HTML**
```html
<form #f="ngForm" (ngSubmit)="mySubmitMethod(f)">
    <!-- Form stuff-->
</form>
```

*#f* is a reference to the form, which is then passed into the submit method

**Typescript**
```ts
onAddItem(form: NgForm) {
    console.log(form);
  }
```

### Validate an input field using Template drive approach

**HTML**
```html
<button [disabled]="!f.valid"></button>
```

*#f* is a reference to the form.  When submitting the form and passing in the reference, it has a *valid* property on it.  If any of the inputs with a required attribute are empty, the *valid* form propety will be false.

### Initialize form with Reactive Forms
**Typescript**
```ts
myForm: FormGroup;

ngOnInit() {
    this.initForm();
}

initForm() {
    this.myForm = new FormGroup(
        { myInput1: new FormControl('', Validators.required) }
        { myInput2: new FormControl('', Validators.required) }
        { myInput3: new FormControl('', Validators.required) }
    );
}
```
**HTML**
```html
<form [formGroup]="myForm" (ngSubmit)="myFormSubmit()">
    <input formControlName="myInput1" type="text">
    <input formControlName="myInput2" type="text">
    <input formControlName="myInput3" type="text">
</form>
```

---

## JavaScript

### parseInt() vs unary +

**Stack Overflow Reference**: <https://stackoverflow.com/questions/17106681/parseint-vs-unary-plus-when-to-use-which>

* Unary + an empty string ('') evaluates to 0
* parseInt() empty string ('') evaluates to NaN
* Unary + is like parseFloat() because it accepts decimals

**Issue Reference**: Working on a coding challenge that checked IPv4 addresses.  I was original using the unary + operator to convert a string to a number, but, when encountering empty strings, I was getting '0' instead of NaN.  As mentioned above, parseInt() had to be used because it converts empty strings to NaN.