esLint中文文档

http://eslint.cn/docs/rules/

```
rules: {
    "no-console": process.env.NODE_ENV === "production" ? "error" : "off",
    "no-debugger": process.env.NODE_ENV === "production" ? "error" : "off",
    semi: ["error", "always"],
    "prettier/prettier": "off"
}
```

