# pj

Simple JSON parser alias for your shell. 

# Installation

place this in your `~/.bashrc` or `~/.zshrc`:

```
alias pj="node -e 'b=require(\"stream\").Transform(),p=process,a=p.argv[1],s=\"\",b._transform=function(p,i,n){s+=\"\"+p,n()},b._flush=function(i){j=JSON.parse(s),a&&a.split(\"/\").map(function(s){j=j[s]||p.exit(-1)}),this.push(JSON.stringify(j,null,\"  \")+\"\n\"),i()},p.stdin.pipe(b).pipe(p.stdout)'"
```

# Usage

`pj` takes JSON-formatted stdin:

```bash
$ echo '{"foo":{"bar":42}}' | pj
{
  "foo": {
    "bar": 42
  }
}
```

You can extract keys by passing the '/' separated JSON path as the first argument:

```bash
$ echo '{"foo":{"bar":42}}' | pj foo
{
  "bar": 42
}
```

```bash
$ echo '{"foo":{"bar":42}}' | pj foo/bar
42
```

Exits with an error code on non-existing keys:

```bash
$ echo '{"foo":{"bar":42}}' | pj foo/bar/badkey ; echo $?
255
```

Works with arrays:

```bash
$ echo '{"foo":[{"bar":45}]}' | pj foo/0
{
  "bar": 45
}
```

# License

Public Domain.








