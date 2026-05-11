# Redis

in `compose.yaml` file:
``` yaml
services:
  redis:
    image: redis
    command: redis-server --requirepass ${REDIS_PASSWORD}
    ports:
      - "${REDIS_PORT}:6379"
  server:
    build:
      context: .
      # target: final
    env_file:
        - .env
    ports:
      - 8080:8080
    environment: 
        - ASPNETCORE_ENVIRONMENT=Development
        - Jwt__Key=${JWT_KEY}
        - ConnectionStrings__DefaultConnection=${SQL_CONNECTION_STRING_DOCKER}
```

in `PrizeService.cs`:

``` C#
public async Task<IEnumerable<ReadPrizeDTO>> GetPrizes(PrizeQParams prizeQParams)
{

    var cachedPrizes = await _cache.GetStringAsync("prizes");

    /// ---- this is the cache ----
    if (!string.IsNullOrEmpty(cachedPrizes))
    {
        var cprizes = JsonSerializer.Deserialize<IEnumerable<ReadPrizeDTO>>(cachedPrizes);
        Console.WriteLine("from cache");
        return cprizes;
    }
    /// ---------------------------
    
    var prizes = await _prizeRepo.GetPrizes(prizeQParams);
    if (prizes == null) return Enumerable.Empty<ReadPrizeDTO>();

    var ttlMinutes = _config.GetValue<int>("CacheSettings:TtlMinutes");
    var options = new DistributedCacheEntryOptions
    {
        AbsoluteExpirationRelativeToNow = TimeSpan.FromMinutes(ttlMinutes)
    };

    var prizesDto = _mapper.Map<IEnumerable<ReadPrizeDTO>>(prizes);
    var serializedPrizes = JsonSerializer.Serialize(prizesDto);

    await _cache.SetStringAsync("prizes", serializedPrizes, options);

    return prizesDto;
}
```