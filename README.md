# frida-compile

Compile a Frida script comprised of one or more Node.js modules without
polluting the global scope.   

This is helpful for multi-script projects that require more modern code
management while also allowing the developer to leverage Frida type definitions
and IDE autocompletion.  

**Please make note of the following**:  

- CommonJS-style imports and exports are no longer supported.  
- The resulting output file is in a bespoke container format and is not meant
  to be valid outside of the context of a Frida Javascript runtime. For the
  curious, [see this test case][test-case].  


## CLI Usage  
```bash
$ frida-compile -h

Usage: frida-compile [options] <module>

Options:
  -o, --output <file>   write output to <file>
  -w, --watch           watch for changes and recompile
  -S, --no-source-maps  omit source-maps
  -c, --compress        compress using terser
  -h, --help            display help for command
```


## Example

```bash
# Create a simple .ts file  
$ echo "console.log('hello, Frida!');" > agent.ts  

# Compile it!  
$ frida-compile agent.ts -o output.js  

# Load it up!  
$ frida -U -f com.example.android --no-pause -l output.js
```


## Installation

```bash
$ npm install frida-compile --save-dev
```

If you're using TypeScript, you'll likely need to install the `@types/frida-gum`
package.  

- [Repository][repo]  
- [NPM][npm]  

```bash
$ npm install @types/frida-gum --save-dev
```


---  


### Development Notes    

- Ensure the build system has Node.js `>= 18.7.0` installed.    
- Configure the submodules  
```bash
$ git submodule init
$ git submodule update
```  
- Build with `make`!  


[test-case]: https://github.com/frida/frida-gum/blob/9580d9da5b06592a7f43c2195b453c39efedf6a7/tests/gumjs/script.c#L9522  

[repo]: https://github.com/DefinitelyTyped/DefinitelyTyped/tree/master/types/frida-gum  

[npm]: https://www.npmjs.com/package/@types/frida-gum  

