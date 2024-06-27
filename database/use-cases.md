# Various DB uses cases

## Column hashing with Generated Column

Take a table of id, primary_number, street_name, street_suffix, city, state, zip_code

And you want an index on `(street_name, street_suffix, city, state, zip_code)`

It may be too big to even create index. It may also be slow since its not a compact index.

What you can do is use a `generated column`, with its value as a md5 hash of these columns

A generated column will be managed by mysql so you don't need to crud on it.

so if you want to search on `(street_name, street_suffix, city, state, zip_code)`, you create a hash on it and go where col_hash = hash

Only problem you can search on just one of these columns you need all of them.

This can be done with a `Functional index`, but Functional indexes are implemented by generated columns.
