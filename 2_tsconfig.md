# tsconfig.json

> tsconfig.json file is always placed in the root of your project and you can customize what rules you want the TypeScript compiler to enforce

```javascript
{
  "compilerOptions": {
    "target": "es2017",
    "module": "commonjs",
    "strictNullChecks": true
  },
  "include": ["**/*.ts"]
}
```

> "strictNullChecks", variables can only have null or undefined values if they are explicitly assigned those values.
