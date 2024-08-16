# Reproduction of Vue + strictTemplates bugs

Demonstrates two bugs with type-checking when strictTemplates is enabled:
- Some fallthrough attributes are not allowed: `id`, `title`, `aria-*`
- Native `@click` event listener not allowed on components that use `defineModel`

```sh
npm install && npm run type-check
```

Results:

```
> vue-project@0.0.0 type-check
> vue-tsc --build --force

src/App.vue:15:37 - error TS2353: Object literal may only specify known properties, and 'id' does not exist in type 'Partial<{}> & Omit<{ readonly msg?: string | undefined; } & VNodeProps & AllowedComponentProps & ComponentCustomProps & Readonly<...>, never>'.

15       <HelloWorld msg="You did it!" id="4" />
                                       ~~

src/App.vue:16:37 - error TS2353: Object literal may only specify known properties, and 'title' does not exist in type 'Partial<{}> & Omit<{ readonly msg?: string | undefined; } & VNodeProps & AllowedComponentProps & ComponentCustomProps & Readonly<...>, never>'.

16       <HelloWorld msg="You did it!" title="my html title" />
                                       ~~~~~

src/App.vue:17:37 - error TS2353: Object literal may only specify known properties, and '"aria-label"' does not exist in type 'Partial<{}> & Omit<{ readonly msg?: string | undefined; } & VNodeProps & AllowedComponentProps & ComponentCustomProps & Readonly<...>, never>'.

17       <HelloWorld msg="You did it!" aria-label="label" />
                                       ~~~~~~~~~~

src/App.vue:19:19 - error TS2353: Object literal may only specify known properties, and 'onClick' does not exist in type 'NonNullable<Partial<{}> & Omit<{ readonly modelValue?: string | null | undefined; "onUpdate:modelValue"?: ((modelValue: string | null) => any) | undefined; } & VNodeProps & AllowedComponentProps & ComponentCustomProps & Readonly<...> & { ...; }, never>>'.

19       <TextInput @click="myFn" />
                     ~~~~~
```
