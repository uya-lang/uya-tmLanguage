# uya-tmLanguage
TextMate grammar for Uya — syntax highlighting for .uya files (used by GitHub Linguist and VS Code) 

- Scope name: `source.uya`
- File extension: `.uya`

## What is covered

| Construct | Example |
| --- | --- |
| Line and block comments | `// …`, `/* … */` |
| Shebang | `#!/usr/bin/env -S uya run` |
| Strings with interpolation | `"Hello, ${name}!"` |
| Raw strings | `` `no escapes here` `` |
| Escape sequences | `\n`, `\xHH`, `\uXXXX` |
| Character literals | `'a'`, `'\x41'` |
| Numeric literals | `0xFF`, `0o755`, `0b1010`, `1_000_000`, `100i8`, `1.5f32` |
| Builtin attributes | `@size_of(T)`, `@align(64)`, `@vector.splat`, `@async_fn` |
| Declaration keywords | `fn`, `struct`, `union`, `interface`, `enum`, `error`, `type`, `use`, `export`, `extern`, `opaque`, `mc`, `test` |
| Control keywords | `if`, `else`, `while`, `for`, `match`, `return`, `try`, `catch`, `defer`, `errdefer`, `as` |
| Modifiers | `const`, `var`, `atomic` |
| Primitive types | `i8`…`i64`, `u8`…`u64`, `usize`, `f32`, `f64`, `byte`, `bool`, `void` |
| Operator families | `+\|`, `-\|`, `*\|`, `+%`, `-%`, `*%`, `\|>`, `=>`, `..`, `->` |
| Type and constant names | `Vec<T>`, `MAX_LEN` |

## Usage

### GitHub Linguist

This repository is the grammar source that Linguist's `grammars.yml` points to,
once Uya is registered as a language. Linguist consumes the grammar through a
git submodule checkout of this repository.

### VS Code

`package.json` declares the language contribution, so this repository can be
used directly as a VS Code extension, with the grammar in `syntaxes/`.

### Other editors

Any editor that accepts TextMate grammars can load
`syntaxes/uya.tmLanguage.json` and register the `source.uya` scope for `.uya`
files.

## Validation

The grammar is checked with the compiler shipped in
[`github-linguist/linguist`](https://github.com/github-linguist/linguist)
(`tools/grammars`):

```bash
# inside linguist/tools/grammars
go build -o grammar-compiler ./cmd/grammar-compiler

grammar-compiler --linguist-path <linguist-root> add vendor/grammars/uya-tmLanguage
```

Expected output:

```
OK! added grammar source 'vendor/grammars/uya-tmLanguage'
	new scope: source.uya
```

## License

MIT. See [LICENSE](LICENSE).
