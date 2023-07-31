### About:
Just a tiny shim to pass `gqlgen`'s calls to `MarshalID` and `UnmarshalID` along to `github.com/rs/xid` for deserialization. Used with `Ent` this results in properly generated, statically typed code with no weirdness.

### Usage:
In `gqlgen.yml`:
```
models:
  ID:
    model:
      - github.com/dsykes16/xidgql.ID
```

### Example Ent Schema/Mixin:
```
package schema

import (
    ...
    "github.com/rs/xid"
)

type XidMixin struct {
    mixin.Schema
}

func (XidMixin) Fields() []ent.Field {
    return []ent.Field{
        field.String("id").
            Immutable().
            Unique().
            GoType(xid.ID{}).
            DefaultFunc(xid.New),
    }
}
```
