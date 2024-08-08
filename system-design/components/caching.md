# Caching

## CDN

CDNs are a kind of cache that comes into play for sites serving large amounts of static media. In a typical CDN setup, a request will first ask the CDN for a piece of static media; the CDN will serve that content if it has it locally available. If it isn't available, the CDN will query the back-end servers for the file, cache it locally, and serve it to the requesting user.

To ensure the content stays up-to-date, the CDN `periodically` checks the origin server for changes and updates its cache accordingly.

See more [here](../../networks/networking-a-top-down-approach/2-application-layer.md#263-content-distribution-networks).

## Cache Invalidation

If the data is modified in the database, it should be invalidated in the cache; if not, this can cause inconsistent application behavior.

### Cache write strategies

#### Cache Aside (AKA Lazy Loading)

The cache does not interact with storage directly. The application does the following:

- Look for entry in cache, resulting in a cache miss
- Load entry from the database
- Add entry to cache
- Return entry

```python
def get_user(self, user_id):
    user = cache.get("user.{0}", user_id)
    if user is None:
        user = db.query("SELECT * FROM users WHERE user_id = {0}", user_id)
        if user is not None:
            key = "user.{0}".format(user_id)
            cache.set(key, json.dumps(user))
    return user
```

Only requested data is cached, which avoids filling up the cache with data that isn't requested.

#### Write-through

The application uses the cache as the main data store, reading and writing data to it, while the cache is responsible for reading and writing to the database.

The process is:

- Application adds/updates entry in cache
- Cache synchronously writes entry to data store
- Return

#### Write-behind (write-back)

Similar to `write-through`, however the cache will asynchronously write to database, so it can return quicker.

The cache places the event in a queue which will pick up the event and write to disk.

### Cache invalidation methods

#### Purge

Removes cached content for a specific object, URL, or a set of URLs. It's typically used when there is an update or change to the content and the cached version is no longer valid.

#### Refresh

Fetch data from db even if in cache and refresh the cache with that data.

#### TTL

The cache checks the time-to-live value and serves the cached content only if the value hasn't expired

#### Stale-while-revalidate

When a request is received for a piece of content, the cached version is immediately served to the user, and an asynchronous request is made to the origin server to fetch the latest version of the content. Once the latest version is available, the cached version is updated.

Used in web browsers and CDNs to serve stale content from the cache while the content is being updated in the background.

### Cache read strategies

#### Read through cache

Application request data from cache directly. If not found in cache, the cache requests from db, updates the cache and returns the response.

#### Read aside cache

Same as [this](#cache-aside-aka-lazy-loading)

### Cache eviction

Applicable when memory limit is reached.

- Least Recently Used (`LRU`): Discards the least recently used items first.
- Least Frequently Used (`LFU`): Counts how often an item is needed. Those that are used least often are discarded first.

- First In First Out (`FIFO`): The cache evicts the first block accessed first without any regard to how often or how many times it was accessed before.
- Last In First Out (`LIFO`): The cache evicts the block accessed most recently first without any regard to how often or how many times it was accessed before.
- Most Recently Used (`MRU`): Discards, in contrast to LRU, the most recently used items first.
- Random Replacement (`RR`): Randomly selects a candidate item and discards it to make space when necessary.
