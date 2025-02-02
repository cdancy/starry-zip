**THE ONLY THING THIS FORK DOES IS USE GO 1.20**

Go zip library
==============

This project is based on the [archive/zip](https://github.com/golang/go/tree/master/src/archive/zip) Go standard library to add a `Updater` struct to allow appending new files to the existing zip archive without decompress the whole file.

Usage
-----

```go
import "github.com/STARRY-S/zip"
```

```go
// Open an existing test.zip archive with read/write only mode for Updater.
f, err := os.OpenFile("test.zip", os.O_RDWR, 0)
handleErr(err)
zu, err := zip.NewUpdater(f)
handleErr(err)
defer zu.Close()

// Updater supports modify the zip comment.
err = zu.SetComment("Test update zip archive")
handleErr(err)

// Append a new file into existing archive.
// The Append method will create a new io.Writer.
w, err := zu.Append("example.txt")
handleErr(err)
// Write data into writer.
_, err = w.Write([]byte("hello world"))
handleErr(err)
```

The completed example test code: [example_updater_test.go](./example_updater_test.go).

License
-------

[BSD 3-Clause](LICENSE)

The zip library is based on [Go standard library](https://github.com/golang/go).
