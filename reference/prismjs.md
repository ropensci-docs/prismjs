# Prism Syntax Highlighter

The `prism_highlight_text` function takes a string with a single code
snippet and returns an html fragment with syntax classes. This html gets
colorized by the [prism stylesheet](https://cdnjs.com/libraries/prism)
when both are inserted in an HTML document.

## Usage

``` r
prism_highlight_text(txt, language = "r")

prism_highlight_document(
  input,
  output = NULL,
  include_css = FALSE,
  preview = interactive()
)

prism_process_xmldoc(doc)

prism_languages()
```

## Arguments

- txt:

  string with code that you want to highlight

- language:

  the language that `txt` is in, one of `prism_languages()`.

- input:

  literal html string, connection, or file path, passed to
  [xml2::read_html](http://xml2.r-lib.org/reference/read_xml.md)

- output:

  path to file or connection to write to, passed to
  [xml2::write_html](http://xml2.r-lib.org/reference/write_xml.md). Set
  `NULL` to return the entire output document as a character string.

- include_css:

  insert the Prism css style (with the default theme) into the html
  header.

- preview:

  opens the generated output html in a browser

- doc:

  an [xml2 document](http://xml2.r-lib.org/reference/read_xml.md) that
  will be modified in place such that all `<code class="language-xyz">`
  elements are replaced with highlighted html.

## Value

html with classes that can be colorized using a prims stylesheet

## Details

The function `prism_highlight_document` processes an entire HTML
document, similar to how PrismJS works in a browser. It automatically
finds all `<code class="language-xyz">` elements in the document and
substitutes these with highlighted html elements. Again, CSS is needed
to actually colorize the html, you can use `include_css` to
automatically inject the CSS in the html header if your input document
does not have this yet.

## Examples

``` r
html <- prism_highlight_text('p { color: red }', language = 'css')
cat(html)
#> <span class="token selector">p</span> <span class="token punctuation">{</span> <span class="token property">color</span><span class="token punctuation">:</span> <span class="token color">red</span> <span class="token punctuation">}</span>
prism_languages()
#>   [1] "plain"                    "plaintext"               
#>   [3] "text"                     "txt"                     
#>   [5] "extend"                   "insertBefore"            
#>   [7] "DFS"                      "markup"                  
#>   [9] "html"                     "mathml"                  
#>  [11] "svg"                      "xml"                     
#>  [13] "ssml"                     "atom"                    
#>  [15] "rss"                      "css"                     
#>  [17] "clike"                    "javascript"              
#>  [19] "js"                       "abap"                    
#>  [21] "abnf"                     "actionscript"            
#>  [23] "ada"                      "agda"                    
#>  [25] "al"                       "antlr4"                  
#>  [27] "g4"                       "apacheconf"              
#>  [29] "sql"                      "apex"                    
#>  [31] "apl"                      "applescript"             
#>  [33] "aql"                      "c"                       
#>  [35] "cpp"                      "arduino"                 
#>  [37] "ino"                      "arff"                    
#>  [39] "armasm"                   "arm-asm"                 
#>  [41] "arturo"                   "art"                     
#>  [43] "asciidoc"                 "adoc"                    
#>  [45] "csharp"                   "cs"                      
#>  [47] "dotnet"                   "aspnet"                  
#>  [49] "asm6502"                  "asmatmel"                
#>  [51] "autohotkey"               "autoit"                  
#>  [53] "avisynth"                 "avs"                     
#>  [55] "avro-idl"                 "avdl"                    
#>  [57] "awk"                      "gawk"                    
#>  [59] "bash"                     "sh"                      
#>  [61] "shell"                    "basic"                   
#>  [63] "batch"                    "bbcode"                  
#>  [65] "shortcode"                "bbj"                     
#>  [67] "bicep"                    "birb"                    
#>  [69] "bison"                    "bnf"                     
#>  [71] "rbnf"                     "bqn"                     
#>  [73] "brainfuck"                "brightscript"            
#>  [75] "bro"                      "bsl"                     
#>  [77] "oscript"                  "cfscript"                
#>  [79] "cfc"                      "chaiscript"              
#>  [81] "cil"                      "cilkc"                   
#>  [83] "cilk-c"                   "cilkcpp"                 
#>  [85] "cilk-cpp"                 "cilk"                    
#>  [87] "clojure"                  "cmake"                   
#>  [89] "cobol"                    "coffeescript"            
#>  [91] "coffee"                   "concurnas"               
#>  [93] "conc"                     "csp"                     
#>  [95] "cooklang"                 "coq"                     
#>  [97] "ruby"                     "rb"                      
#>  [99] "crystal"                  "csv"                     
#> [101] "cue"                      "cypher"                  
#> [103] "d"                        "dart"                    
#> [105] "dataweave"                "dax"                     
#> [107] "dhall"                    "diff"                    
#> [109] "markup-templating"        "django"                  
#> [111] "jinja2"                   "dns-zone-file"           
#> [113] "dns-zone"                 "docker"                  
#> [115] "dockerfile"               "dot"                     
#> [117] "gv"                       "ebnf"                    
#> [119] "editorconfig"             "eiffel"                  
#> [121] "ejs"                      "eta"                     
#> [123] "elixir"                   "elm"                     
#> [125] "lua"                      "etlua"                   
#> [127] "erb"                      "erlang"                  
#> [129] "excel-formula"            "xls"                     
#> [131] "xlsx"                     "fsharp"                  
#> [133] "factor"                   "false"                   
#> [135] "firestore-security-rules" "flow"                    
#> [137] "fortran"                  "ftl"                     
#> [139] "gml"                      "gamemakerlanguage"       
#> [141] "gap"                      "gcode"                   
#> [143] "gdscript"                 "gedcom"                  
#> [145] "gettext"                  "po"                      
#> [147] "gherkin"                  "git"                     
#> [149] "glsl"                     "gn"                      
#> [151] "gni"                      "linker-script"           
#> [153] "ld"                       "go"                      
#> [155] "go-module"                "go-mod"                  
#> [157] "gradle"                   "graphql"                 
#> [159] "groovy"                   "haml"                    
#> [161] "handlebars"               "hbs"                     
#> [163] "mustache"                 "haskell"                 
#> [165] "hs"                       "haxe"                    
#> [167] "hcl"                      "hlsl"                    
#> [169] "hoon"                     "http"                    
#> [171] "hpkp"                     "hsts"                    
#> [173] "ichigojam"                "icon"                    
#> [175] "icu-message-format"       "idris"                   
#> [177] "idr"                      "ignore"                  
#> [179] "gitignore"                "hgignore"                
#> [181] "npmignore"                "inform7"                 
#> [183] "ini"                      "io"                      
#> [185] "j"                        "java"                    
#> [187] "php"                      "javadoclike"             
#> [189] "javadoc"                  "javastacktrace"          
#> [191] "jexl"                     "jolie"                   
#> [193] "jq"                       "typescript"              
#> [195] "ts"                       "jsdoc"                   
#> [197] "json"                     "webmanifest"             
#> [199] "json5"                    "jsonp"                   
#> [201] "jsstacktrace"             "julia"                   
#> [203] "keepalived"               "keyman"                  
#> [205] "kotlin"                   "kt"                      
#> [207] "kts"                      "kumir"                   
#> [209] "kum"                      "kusto"                   
#> [211] "latex"                    "tex"                     
#> [213] "context"                  "latte"                   
#> [215] "less"                     "scheme"                  
#> [217] "lilypond"                 "ly"                      
#> [219] "liquid"                   "lisp"                    
#> [221] "elisp"                    "emacs"                   
#> [223] "emacs-lisp"               "livescript"              
#> [225] "llvm"                     "log"                     
#> [227] "lolcode"                  "magma"                   
#> [229] "makefile"                 "markdown"                
#> [231] "md"                       "mata"                    
#> [233] "matlab"                   "maxscript"               
#> [235] "mel"                      "mermaid"                 
#> [237] "metafont"                 "mizar"                   
#> [239] "mongodb"                  "monkey"                  
#> [241] "moonscript"               "moon"                    
#> [243] "n1ql"                     "n4js"                    
#> [245] "n4jsd"                    "nand2tetris-hdl"         
#> [247] "naniscript"               "nani"                    
#> [249] "nasm"                     "neon"                    
#> [251] "nevod"                    "nginx"                   
#> [253] "nim"                      "nix"                     
#> [255] "nsis"                     "objectivec"              
#> [257] "objc"                     "ocaml"                   
#> [259] "odin"                     "opencl"                  
#> [261] "openqasm"                 "qasm"                    
#> [263] "oz"                       "parigp"                  
#> [265] "parser"                   "pascal"                  
#> [267] "objectpascal"             "pascaligo"               
#> [269] "psl"                      "pcaxis"                  
#> [271] "px"                       "peoplecode"              
#> [273] "pcode"                    "perl"                    
#> [275] "phpdoc"                   "plant-uml"               
#> [277] "plantuml"                 "plsql"                   
#> [279] "powerquery"               "pq"                      
#> [281] "mscript"                  "powershell"              
#> [283] "processing"               "prolog"                  
#> [285] "promql"                   "properties"              
#> [287] "protobuf"                 "pug"                     
#> [289] "puppet"                   "pure"                    
#> [291] "purebasic"                "pbfasm"                  
#> [293] "purescript"               "purs"                    
#> [295] "python"                   "py"                      
#> [297] "qsharp"                   "qs"                      
#> [299] "q"                        "qml"                     
#> [301] "qore"                     "r"                       
#> [303] "racket"                   "rkt"                     
#> [305] "cshtml"                   "razor"                   
#> [307] "jsx"                      "tsx"                     
#> [309] "reason"                   "regex"                   
#> [311] "rego"                     "renpy"                   
#> [313] "rpy"                      "rescript"                
#> [315] "res"                      "rest"                    
#> [317] "rip"                      "roboconf"                
#> [319] "robotframework"           "robot"                   
#> [321] "rust"                     "sas"                     
#> [323] "sass"                     "scss"                    
#> [325] "scala"                    "shell-session"           
#> [327] "shellsession"             "sh-session"              
#> [329] "smali"                    "smalltalk"               
#> [331] "smarty"                   "sml"                     
#> [333] "smlnj"                    "solidity"                
#> [335] "sol"                      "solution-file"           
#> [337] "sln"                      "soy"                     
#> [339] "turtle"                   "trig"                    
#> [341] "sparql"                   "rq"                      
#> [343] "splunk-spl"               "sqf"                     
#> [345] "squirrel"                 "stan"                    
#> [347] "stata"                    "iecst"                   
#> [349] "stylus"                   "supercollider"           
#> [351] "sclang"                   "swift"                   
#> [353] "systemd"                  "t4-templating"           
#> [355] "t4-cs"                    "t4"                      
#> [357] "vbnet"                    "t4-vb"                   
#> [359] "yaml"                     "yml"                     
#> [361] "tap"                      "tcl"                     
#> [363] "tt2"                      "textile"                 
#> [365] "toml"                     "tremor"                  
#> [367] "troy"                     "trickle"                 
#> [369] "twig"                     "typoscript"              
#> [371] "tsconfig"                 "unrealscript"            
#> [373] "uscript"                  "uc"                      
#> [375] "uorazor"                  "uri"                     
#> [377] "url"                      "v"                       
#> [379] "vala"                     "velocity"                
#> [381] "verilog"                  "vhdl"                    
#> [383] "vim"                      "visual-basic"            
#> [385] "vb"                       "vba"                     
#> [387] "warpscript"               "wasm"                    
#> [389] "web-idl"                  "webidl"                  
#> [391] "wgsl"                     "wiki"                    
#> [393] "wolfram"                  "mathematica"             
#> [395] "wl"                       "nb"                      
#> [397] "wren"                     "xeora"                   
#> [399] "xeoracube"                "xojo"                    
#> [401] "xquery"                   "yang"                    
#> [403] "zig"                     
```
