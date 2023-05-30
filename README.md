# Angular 15

## Standalone Components (no module anymore)

FROM: https://www.youtube.com/watch?v=uY_Cy_wUmQI
(But no nx used here)

0. ng new myApp
1. Disable content of AppModule
2. Change main.ts:

OLD:

```typescript
// platformBrowserDynamic().bootstrapModule(AppModule)
//   .catch(err => console.error(err));
```

NEW:

```typescript
bootstrapApplication(AppComponent)
    .catch( err => console.error(err))
```

3. Run app to check if it works
4. Add new standalone component: `ng g c MyCmp --standalone`
5. Add new component to imports of `app.component.ts`:

    ```typescript
    imports: [MyCmpComponent],
    ```

6. Add ui of new component to `app.component.html`:

    ```html
    <app-my-cmp></app-my-cmp>
    ```

7. Run app to check if it works

## Debug Validation Errors

```ts
  getAllFormValidationErrors(): any {
    return this.getFormValidationErrors(this.myFormGroup);
  }

  getFormValidationErrors(form: FormGroup) {
    const result: any[] = [];
    Object.keys(form.controls).forEach(key => {
      const controlErrors: ValidationErrors | null | undefined = form.get(key)?.errors;

      if (controlErrors) {
        Object.keys(controlErrors).forEach(keyError => {
          result.push({
            control: key,
            error: keyError,
            value: controlErrors[keyError]
          });
        });
      }
    });

    return result;
  } 
```

```html
<pre>{{ myFormGroup.valid | json }}</pre>
<pre>{{ control1.value | json }}</pre>
<pre>{{ control1.errors | json }}</pre>
<pre>{{ control2.value | json }}</pre>
<pre>{{ control2.errors | json }}</pre>
<pre>{{ getAllFormValidationErrors() | json }}</pre>
```
