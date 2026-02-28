# ~~~LuaO~~~
Documentation:

# JAVASCRIPT!!!!!:
```const { url } = await fetch(`https://raw.githubusercontent.com/xlum20/LuaO/refs/heads/main/tunnel-url.json'
).then(r => r.json());

const res = await fetch(`${url}/transpile`, {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({ code: 'local x: number = 5' })
});

const { result } = await res.json();
console.log(result);
```

# CURL / BASH:
```URL=$(curl -s https://raw.githubusercontent.com/xlum20/LuaO/refs/heads/main/tunnel-url.json | python3 -c "import sys,json; print(json.load(sys.stdin)['url'])")

curl -X POST "$URL/transpile" \
  -H "Content-Type: application/json" \
  -d '{"code": "local x: number = 5"}'
  ```

  # LUA:
```local json = require("json") -- or use your json lib

local function getUrl()
  local handle = io.popen("curl -s https://raw.githubusercontent.com/xlum20/LuaO/refs/heads/main/tunnel-url.json")
  local raw = handle:read("*a")
  handle:close()
  return raw:match('"url"%s*:%s*"([^"]+)"')
end

local function transpile(code)
  local url = getUrl()
  local escaped = code:gsub('"', '\\"')
  local cmd = string.format(
    'curl -s -X POST "%s/transpile" -H "Content-Type: application/json" -d "{\\"code\\":\\"%s\\"}"',
    url, escaped
  )
  local handle = io.popen(cmd)
  local result = handle:read("*a")
  handle:close()
  return result:match('"result"%s*:%s*"(.-[^\\])"')
end

print(transpile("local x: number = 5"))```
