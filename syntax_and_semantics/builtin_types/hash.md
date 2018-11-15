# Hash

## Existent key

`hash{key}` where `hash` doesn't have `key` will be `nil`, but the value also might be nil for the key.
Therefore, a key can be checked if it exists in a hash using the syntax: `hash.exists(key)`.

## Deleting a key

A key can be deleted from a hash using the syntax: `hash.delete(key)`.
