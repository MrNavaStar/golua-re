# Golua Regex

This extension to [Aarzilli's Golua](http://github.com/aarzilli/golua) adds 
Unicode and Regex support to all functions from the Lua string library.

Lua patterns can be replaced by [Go regexps](http://github.com/google/re2/wiki/Syntax). This breaks
compatibility with Lua. If this is undesired, simply register the library under a different alias

## Example

``` go
package main

import (
	"github.com/mrnavastar/goluare"
	"github.com/aarzilli/golua/lua"
)

func main() {
	L := lua.NewState()
	defer L.Close()
	L.OpenLibs()
	L.RegisterLib("string", goluare.REGEX)

	L.DoString(`print(string.len("résumé"))`)
	L.DoString(`print(string.upper("résumé"))`)
	L.DoString(`print(string.gsub("résumé", "\\pL", "[$0]"))`)
}
```
