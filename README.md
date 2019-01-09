# Be.IO

Be.IO is a fast big-endian implementation of .NET's BinaryReader and BinaryWriter.

## Getting Started

First, add this using statement at the top of your file:

```csharp
using Be.IO;
```

After that, you can use `BeBinaryWriter` and `BeBinaryReader` the same way you would use a regular binary reader/writer. Example:

```csharp
using (var file = File.Open("foo.txt", FileMode.Create))
{
    var writer = new BeBinaryWriter(file);
    writer.WriteInt16(0x1357);
    writer.WriteInt32(0xDEADBEEF);
    writer.WriteInt64(long.MinValue);
    
    var reader = new BeBinaryReader(file);
    short s = reader.ReadInt16();
    int i = reader.ReadInt32();
    long l = reader.ReadInt64();
}
```

## WARNING!

Character-based methods like `ReadString` still read characters in little-endian. This is because the `Encoding` you pass into the stream reader/writer is responsible for converting characters to bytes and vice versa, so it gets to choose which endian to use. If you need to read/write in an encoding that is endian-sensitive (like UTF-16), you'll have to find a big-endian version of that encoding.

## License?

Be.IO is licensed under the [BSD simplified license](license.bsd).
