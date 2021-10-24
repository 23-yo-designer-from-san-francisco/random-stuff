File extensions

```bash
~% FILE="example.tar.gz"

~% echo "${FILE%%.*}"
example

~% echo "${FILE%.*}"
example.tar

~% echo "${FILE#*.}"
tar.gz

~% echo "${FILE##*.}"
gz
```

Parallel encoding with Makefile

```make
all: $(patsubst %.m4a,%.opus,$(wildcard *.m4a))
.PHONY: all
%.opus: %.m4a
	ffmpeg -i $< -f wav - | opusenc - $@
```

Count files

```bash
find . -name "*.m4a" -printf '.' | wc -m
```
