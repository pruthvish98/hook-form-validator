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
