---
title: Unique GitHub repositories containing path
---

How can I find all my repositories on GitHub which contain a file or folder?

Note, it shouldn't search for the path in the description or the file contents.

```js
const ACCESS_TOKEN = "...";
const USERNAME = "...";
const PATH = "..."

const API_URL = `https://api.github.com/search/code?q=path:${PATH}+user:${USERNAME}`;
const API_HEADERS = {
  "Authorization": `token ${ACCESS_TOKEN}`
};

async function searchCode(url: string, headers: { [key: string]: string }) {
  try {
    const response = await fetch(url, { headers });
    
    if (response.ok) {
      const data = await response.json();

      return data;
    } else {
      console.log("API error:", response.status);
    }
  } catch (error) {
    console.error("Fetch error:", error);
  }
}

const data = await searchCode(API_URL, API_HEADERS);

const uniqueRepos = new Set();

for (const item of data.items) {
  const name = item.repository.full_name;
  uniqueRepos.add(name);
}

console.log(`GitHub repositories of user '${USERNAME}' containing path '${PATH}':`);

for (const item of uniqueRepos) {
  console.log(item)
}
```
