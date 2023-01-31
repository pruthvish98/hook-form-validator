# hook-form-validator

A fast and lightweight,free and open-source validation library for ReactJS that addresses three primary form creation pain points: State manipulation. Form Validation (error message) Form Submission.

This library consists wrapper React components over <a href="https://github.com/pruthvish98/hook-form-validator"> hook-form-validator </a> library.

**Show**
### <a href="https://react-validation-hook.vercel.app/">Demo page</a>

### Installation

```shell
npm i hook-form-validator
```

```shell
npm i deepmerge
```

## Usage

#### JSX


```jsx
import React, { Component } from 'react';
import * as Yup from "yup";
import useValidator  from 'hook-form-validator';

export default function App() {

  const onSubmit = () => {
   // here you will get the validated data
   console.log(values)
  }

  const {
    values,
    setValues,
    touched,
    errors,
    handleSubmit,
    getFieldProps,
  } = useValidator({
    initialValues: {
      username: "",
      email: "",
    },
    validationSchema: Yup.object({
      username: Yup.string().required("User Name is Required."),
      email: Yup.string().email().required("Email is Required."),
    }),
    onSubmit,
  });


  return (
    <>
        <form onSubmit={handleSubmit}>
          <div>
             <input type="text" name="username" {...getFieldProps("username")} />
             {(touched?.username && errors?.username) && <div>{errors?.username}</div>}
          </div>

          <div>
             <input type="text" name="email" {...getFieldProps("email")} />
             {(touched?.email && errors?.email) && <div>{errors?.email}</div>}
          </div>
  
          <button type="submit">
            Save
          </button>
        </form>
    </>
  );
}
```

## API

### **Container**

Component that contains the draggable elements or components. Each of its children should be wrapped by **Draggable** component


### Function

| Property | Type | Default | Description |
|-|:-:|:-:|-|
|values|object|`{}`| Get updated values
|errors|object|`{}` | Get all the errors
|touched|object|`{}`| It helps to display error based on blur event
|setValues|function|`undefined`| Update the values
|getFieldProps|function|`undefined`| You can directly pass this function for handle the value
|setErrors|function|`undefined`| It helps to update errors manually. 
|handleChange|function|`undefined`| It trigger the manually onChange function with help of createFakeEvent
|handleBlur|function| `undefined` | It trigger the manually onBlur function with help of createFakeEvent
|handleSubmit|function|`undefined`| You have pass this function in form tag
|createFakeEvent|function|`undefined`| It will helps to trigger fake event

---


---

### handleSubmit
  You have pass this function in form tag with the help of this function it trigger when submit button is clicked & check for errors & trigger the onSubmit function which is provided by our hook

```js

You can see the example to use handleSubmit

```

#### Parameters
- **handleSubmit** : `handleSubmit`  




### setValues
 
This function use to update the initialValues  


```
setValue({...values,[key]:[value]})
```

```js
const App = () => {
  const {
     setValues,
     handleSubmit,
     getFieldProps,
  } = useValidator({
    initialValues: {
      firstName: "",
    },
    validationSchema: Yup.object({
      firstName: Yup.string().required("User Name is Required."),
    }),
    onSubmit,
  });
    return (
    <form>
      <input {...getFieldProps("firstName")} />
      <button type="button" onClick={() => setValue("firstName", "Bill")}>
        setValue
      </button>
    </form>
  );
};
```


#### Parameters
- **payload** : `object` 

---

### getFieldProps
 
You can directly pass this function for handle the value

```js

<input {...getFieldProps('firstName')} />
```

#### Parameters
- **onChange** : `ChangeHandler`  onChange prop to subscribe the input change event.
- **onBlur** : `ChangeHandler`    onBlur prop to subscribe the input blur event.
- **ref** : `React.Ref<any>`      Input reference for hook form to register.
- **name** : `string`             Input's name being registered.



---

### setErrors
 
The function allows you to manually set one or more errors with your custom message.

```js
setErrors({...errors,[key]:[message]})
```

#### Parameters
- **errors** : `errors`  Set an error with its type and message.




---

### handleChange
  It trigger the manually onChange function with help of createFakeEvent.

```js
<input 
  onChange={(e) => {
    handleChange("firstName")(createFakeEvent(e));
  }}
/>

```

#### Parameters
- **handleChange** : `handleChange`  



---

### handleBlur
  It trigger the manually onBlur function with help of createFakeEvent.

```js
<input 
  onChange={(e) => {
    handleBlur("firstName")(createFakeEvent(e));
  }}
/>

```

#### Parameters
- **handleBlur** : `handleBlur`  

