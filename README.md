# LuaO
Documentation:
const { url } = await fetch(
  'https://raw.githubusercontent.com/xlum20/LuaO/main/tunnel-url.json'
).then(r => r.json());

const res = await fetch(`${url}/transpile`, {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({ code: 'local x: number = 5' })
});
