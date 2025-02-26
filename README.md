This is Leonard Kleinrock's network simulator.  He wrote this on the
TX-2 as part of the research reported in his thesis,
[Message Delay in Communication Nets with
Storage](https://www.lk.cs.ucla.edu/data/files/Message%20delay%20Phd.pdf).

We're in the process of transcribing both the assembly-language source
code and also the binary, from a listing.  We should be able to use
each to check the other.

The files are:

- FREQ6FR.tx2as: assembly-language source code in a Unicode-friendly
  format
- binary-data.txt: the octal data and address information from the
  listing.

The binary data can be converted into a TX-2 tape image file with the
`tx2maketape` tool from https://github.com/TX-2/TX-2-simulator:

```
cargo  run --bin tx2maketape --  Kleinrock-network-simulator/binary-data.txt  --output=kns.tape
```

The `tx2maketape` tool accepts a command-line option indicating the
addres at which the program should be started; the default start
address is probably not useful.  You can also disassemble the tape
image using the disassembler:

```
cargo  run --bin tx2dis --  kns.tape
```

You should be able to assemble the assembly source like this:

```
cargo run --bin  tx2m4as -- --list --output kns.tape Kleinrock-network-simulator/FREQ6FR.tx2as
```

Unfortunately, due to the current limitations in the assembler, this
doesn't work yet.
