# Iframe Test Playground

A static website with many iframe cases for practicing UI test automation.

## Put it online with GitHub Pages
1. Create a new **public** repository on GitHub (for example `iframe-test-site`).
2. Click **Add file → Upload files**, drag in everything from this folder (index.html, css, frames, .nojekyll, README.md), then click **Commit changes**.
3. Go to **Settings → Pages**. Under *Build and deployment*, choose **Deploy from a branch**, branch **main**, folder **/ (root)**, then **Save**.
4. Wait 1–2 minutes. Your site will be at `https://yashcqa.github.io/iframeTest/`.

## Test cases
| Section | Iframe id | What to test |
|---|---|---|
| Login form | `frame-form` | Type, click, read result (`tester` / `password123`) |
| Buttons | `frame-buttons` | Counter, alert/confirm/prompt, delayed text |
| Nested | `frame-outer` → `frame-inner` | Switching into a frame inside a frame |
| Table | `frame-table` | Read cells, search box, dropdown filter |
| Dynamic | `frame-dynamic` | Iframe appears 2s after clicking Load |
| srcdoc | `frame-srcdoc` | Inline iframe content |
| postMessage | `frame-message` | Parent ↔ iframe messages |
| Same page twice | `frame-copy-1`, `frame-copy-2` | Choosing the right frame |

## Playwright example
```js
const frame = page.frameLocator('#frame-form');
await frame.getByTestId('username').fill('tester');
await frame.getByTestId('password').fill('password123');
await frame.getByTestId('btn-login').click();
await expect(frame.getByTestId('login-result')).toHaveText('Signed in as tester');

// nested
const inner = page.frameLocator('#frame-outer').frameLocator('#frame-inner');
await inner.getByTestId('inner-input').fill('hi');
```

## Selenium (Python) example
```python
driver.switch_to.frame("frame-outer")
driver.switch_to.frame("frame-inner")
driver.find_element(By.ID, "inner-input").send_keys("hi")
driver.switch_to.default_content()
```
