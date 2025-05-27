# Virtual-Piano-Skipper
This script is created to help play those impossible notes on VirtualPiano.net. There are always those note combos that are just impossible to play on a keyboard, either because the keyboard can't handle those many keys pressed together, or cause finger positioning are almost impossible, or simply because you have to mix a shifted and unshifted key together. 
This script will allow you to simulate playing those notes to skip through without ruining the melody and your flow.

# How does this work
You press **Ctrl** button on your keyboard and the currently highlighted note automatically gets played, regardless of whether it's a combo of 10 keys or just a single key. Think of it as a skip button. 

# How to use
1. In your browser open inspect (right click anywhere and choose the Inspect/Inspect element option)
2. Go to console tab
3. Paste the following script in there and press Enter
```
function getKeyCode(char) { const upper = char.toUpperCase(); if (/[A-Z]/.test(upper)) return upper.charCodeAt(0); if (/[0-9]/.test(char)) return char.charCodeAt(0); const keyCodeMap = { '%': 53, '@': 50, '#': 51, '!': 49, '&': 55, '*': 56, '(': 57, ')': 48, '^': 54, '$': 52, '+': 187, '=': 187, '-': 189, '_': 189, '[': 219, ']': 221, '{': 219, '}': 221, '\\': 220, '|': 220, ';': 186, ':': 186, "'": 222, '"': 222, ',': 188, '<': 188, '.': 190, '>': 190, '/': 191, '?': 191, '`': 192, '~': 192 }; return keyCodeMap[char] || 0; } function getCode(char) { const upper = char.toUpperCase(); if (/[A-Z]/.test(upper)) return 'Key' + upper; if (/[0-9]/.test(char)) return 'Digit' + char; const codeMap = { '%': 'Digit5', '@': 'Digit2', '#': 'Digit3', '!': 'Digit1', '&': 'Digit7', '*': 'Digit8', '(': 'Digit9', ')': 'Digit0', '^': 'Digit6', '$': 'Digit4', '+': 'Equal', '=': 'Equal', '-': 'Minus', '_': 'Minus', '[': 'BracketLeft', '{': 'BracketLeft', ']': 'BracketRight', '}': 'BracketRight', '\\': 'Backslash', '|': 'Backslash', ';': 'Semicolon', ':': 'Semicolon', "'": 'Quote', '"': 'Quote', ',': 'Comma', '<': 'Comma', '.': 'Period', '>': 'Period', '/': 'Slash', '?': 'Slash', '`': 'Backquote', '~': 'Backquote' }; return codeMap[char] || 'Unidentified'; } function needsShift(char) { return /[A-Z~!@#$%^&*()_+{}|:"<>?]/.test(char); } function simulateKeyCombination(inputStr) { for (let i = 0; i < inputStr.length; i++) { const char = inputStr[i]; const shift = needsShift(char); const code = getCode(char); const keyCode = getKeyCode(char); const options = { key: char, code: code, keyCode: keyCode, which: keyCode, ctrlKey: false, shiftKey: shift, bubbles: true, cancelable: true }; const keydown = new KeyboardEvent('keydown', options); document.dispatchEvent(keydown); const keyup = new KeyboardEvent('keyup', options); document.dispatchEvent(keyup); } } $(document).on('keydown', function (e) { if (e.ctrlKey && !e.repeat) { var keys = $('#song-pattern .active').text(); simulateKeyCombination(keys); } });
```
4. Close the console and enjoy
