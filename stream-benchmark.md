Compile and run (debian, ubuntu, termux, ...)
```bash
wget https://www.cs.virginia.edu/stream/FTP/Code/stream.c && gcc -fopenmp -D_OPENMP stream.c -O3 -o stream -DNTIMES=100 && ./stream
```

Compile on macOS

```bash
brew install llvm
```

```bash
/opt/homebrew/Cellar/llvm/13.0.0_1/bin/clang -fopenmp -D_OPENMP stream.c -O3 -o stream -L/opt/homebrew/Cellar/libomp/13.0.0/lib
```
