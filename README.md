# almide/toml

TOML v1.0 parser and serializer for [Almide](https://github.com/almide/almide). Pure Almide implementation with Codec integration.

## Install

```bash
almide add toml
```

## Usage

```almide
import toml

// Parse TOML text
let config = toml.parse("""
[server]
host = "localhost"
port = 8080
debug = false
""")!

// Stringify Value to TOML
let text = toml.stringify(config)
```

### With Codec

```almide
import toml

type ServerConfig: Codec = { host: String, port: Int, debug: Bool }

// Encode a typed record to TOML string
let text = toml.encode(ServerConfig { host: "0.0.0.0", port: 3000, debug: true })

// Decode TOML string to a typed record
let config = ServerConfig.decode(toml.parse(text)!)!
```

## API

| Function | Signature | Description |
|---|---|---|
| `toml.parse` | `(String) -> Result[Value, String]` | Parse TOML text into a Value |
| `toml.stringify` | `(Value) -> String` | Serialize a Value to TOML text |
| `toml.encode` | `(T: Codec) -> String` | Encode a Codec type to TOML (via Codec protocol) |
| `toml.decode[T]` | `(String) -> Result[T, String]` | Decode TOML to a Codec type (via Codec protocol) |

`encode` and `decode` work automatically with any type that derives `Codec` — no extra implementation needed.

## Supported TOML Features

- Strings: basic (`"..."`), literal (`'...'`), multiline (`"""..."""`, `'''...'''`)
- Numbers: integers, floats, hex/octal/binary, underscore separators, `nan`, `inf`
- Booleans, datetimes (stored as strings)
- Tables, nested tables, dotted keys
- Arrays, array of tables (`[[...]]`)
- Inline tables
- Comments

## License

MIT
