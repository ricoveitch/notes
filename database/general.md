# General Notes

## Collation

Collations are a set of rules that decide how characters compare to each other. A set of rules.

The default in mysql is `utf8mb4_0900_ai_ci`.

- `utf8mb4`: name of the character set
- `0900`: unicode weights
- `ai`: accent insensitive (à == a)
- `ci`: character insensitive (A == a)

## Planet scale boost

TOREAD: https://planetscale.com/blog/how-planetscale-boost-serves-your-sql-queries-instantly

Pretty much caching the results.

You have a query that is slow

Take the query and invert it to see how the result of that query change, should someone write data to the underling database

Subscribe to those writes (changes), and can change that cached value, so when you query its up to date